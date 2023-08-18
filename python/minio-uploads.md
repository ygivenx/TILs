# Minio uploads using Flask

A very common problem is to be able to upload a large file to a webapp. Minio provides a way to do this.

The example code snippet can be used within a flask app to upload file to minio.

```python
from minio import Minio
from dotenv import dotenv_values

# get Minio credentials
config = dotenv_values(".env")

client = Minio(
    f'{config["MINIO_HOST"]}:{config["MINIO_PORT"]}',
    access_key=config["MINIO_ACCESS_KEY"],
    secret_key=config["MINIO_SECRET_KEY"],
    secure=False # should be true for prod or AWS
)

# create bucket
if not client.bucket_exists(config["BUCKETNAME"]):
    client.make_bucket(config["BUCKETNAME"])
else:
    print(f"Bucket {config['BUCKETNAME']} already exists")

# upload file to Minio
# from Flask app
# this will be inside a function which handle upload
if "file" in request.files:  # file upload name 
    uploaded_file = request.files["file"]
    if uploaded_file:
        size = os.fstat(uploaded_file.fileno()).st_size
        client.put_object(
            config['BUCKETNAME'],
            secure_filename(uploaded_file.filename),
            uploaded_file,
            size)
```