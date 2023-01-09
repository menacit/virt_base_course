FROM python:3.11.0

RUN pip install Flask==2.2.2
COPY app.py .

USER 10000
CMD ["flask", "run", "--host", "0.0.0.0"]
