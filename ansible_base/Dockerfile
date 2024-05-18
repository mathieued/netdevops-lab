FROM python:3

WORKDIR /usr/src/app
COPY ansible_base/requirements_base.txt ./

RUN pip install --no-cache-dir -r requirements_base.txt

CMD ["python"]