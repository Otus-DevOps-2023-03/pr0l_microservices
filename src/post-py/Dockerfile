FROM python:3.10-alpine

WORKDIR /app
ADD . /app

ENV POST_DATABASE_HOST post_db
ENV POST_DATABASE posts

RUN apk --no-cache --update add build-base && \
    pip install -r /app/requirements.txt && \
    apk del build-base



ENTRYPOINT ["python3", "post_app.py"]
