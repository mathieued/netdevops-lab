FROM mathieued/ansible_base:latest

WORKDIR /usr/src/app
COPY requirements.txt ./

RUN pip install --no-cache-dir -r requirements.txt

CMD ["python"]