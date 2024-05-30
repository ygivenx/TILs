# Python RQ

A simple getting started for python RQ. RQ is a simple library that use can be used to create a queue to process long running tasks.

### Steps

- Run a redis docker
`docker run -d --name redis-test -p 6379:6379 redis:latest`

-  Start a rq worker
`rq worker -u redis://localhost:6379/0`
 
- Create a python file with a task and process the results.
```python
# task.py
from redis import Redis
from rq import Queue
from rq.job import Job
import time
import random
from dummy_task import simple_task

# Connect to Redis
redis_conn = Redis.from_url("redis://localhost:6379/0")


def fetch_result(job_id):
    job = Job.fetch(id=job_id, connection=redis_conn)
    if job.is_finished:
        print(job.return_value())
    else:
        job.get_status()


if __name__ == "__main__":
    q = Queue(connection=redis_conn)
    job_ids = []
    for i in range(1000):
        result = q.enqueue(simple_task, random.randint(1, 100), random.randint(1, 100))
        job_ids.append(result.id)

    time.sleep(10)
    for job_id in job_ids:
        fetch_result(job_id)
```

Hope this helps! ⭐️

---
Keep Building!

Rohan 