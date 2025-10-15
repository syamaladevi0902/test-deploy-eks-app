# Stage 1: build (install dependencies)
FROM python:3.12-slim as builder
WORKDIR /app
# install build deps
COPY app/requirements.txt .
RUN pip install --user -r requirements.txt
COPY ..

# Stage 2: runtime
FROM python:3.12-slim
WORKDIR /app
# copy installed packages from builder
COPY --from=builder /root/.local /root/.local
COPY --from=builder /app /app
ENV PATH=/root/.local/bin:$PATH
EXPOSE 5000
CMD ["python", "main.py"]
