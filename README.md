# Compare Docker Image Build: PIP vs UV

## Docker image build

### PIP

```docker
FROM python:3.12-slim

LABEL maintainer="Supphachoke Suntiwichaya <mrchoke@gmail.com>"

COPY requirements.txt /requirements.txt
RUN pip install -r /requirements.txt

CMD ["pip", "freeze"]
```

```
docker build --no-cache -t test:pip -f Dockerfile.pip .
```

![pip build](pip.jpg)

### UV

```docker
FROM python:3.12-slim

LABEL maintainer="Supphachoke Suntiwichaya <mrchoke@gmail.com>"

COPY requirements.txt /requirements.txt
RUN pip install uv \
  && uv pip install --system -r /requirements.txt

CMD ["uv", "pip", "list", "--format" ,"freeze"]
```

```
docker build --no-cache -t test:uv -f Dockerfile.uv .
```

![uv build](uv.jpg)

## Result

### Time

| Type | Build | Stage3/3 |
| ---- | ----- | -------- |
| pip  | 31s   | 15.4s    |
| uv   | 18s   | 4.2s     |

### Size

| Type | Size  |
| ---- | ----- |
| pip  | 813MB |
| uv   | 655MB |

![image size](image-size.jpg)
