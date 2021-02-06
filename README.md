### Image resizer web app

##### Checkout the live version (DEPRECATED)
- ~~http://ec2-3-86-86-236.compute-1.amazonaws.com~~

##### Requirements:

- Python 3.6.5
- Yarn

---

##### How to run:

- Clone the repo.
- Use the command `git submodule update --init --recursive` to get the frontend and backend.
- Inside `image-resizer-api` checkout master with `git checkout master`, the same for the `image-resizer-front`
- Go to `ìmage-resizer-api` folder and change the permission of `boot.sh` file with the command `sudo chmod +x boot.sh`.
- Go to `image-resizer-front` and use `yarn install` command to install dependecies.
- Use `pip install docker-compose`.
- Use `docker-compose build` and `docker-compose up`

Both containers front-end and back-end are running @`http://localhost:8080` @`http://localhost:8000` respectively. Check the front-end to test the application.

---

##### Architecture:

Basically:

- **Django** API, **RabbitMQ** for Async tasks, **Vue** Client.
- The resize task is handled by the **OpenCV** library.

---

##### Flow:

- Front-end sends the payload with "file", "name", "width", "height"
- Back-end will save this file instance.
- Back-end then sends the file to the RabbitMQ and celery does the "resize_job" asynchronously.
- While this job is in progress the front-end will check every 2 seconds whether the "job_done" property is true. "job_done" can be fetched @`/api/images/{job_id}/` endpoint in the API.
- If job is done the frontend will then catch the resized image url and show a download button.
