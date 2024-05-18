FROM python:3.13-rc-alpine

WORKDIR /usr/src/app
COPY requirements_base.txt ./

RUN pip install --no-cache-dir -r requirements_base.txt

CMD ["python"]