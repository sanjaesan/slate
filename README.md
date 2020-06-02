
Docker 
------------
docker run -d --rm --name slate -p 4567:4567 -v $(pwd)/build:/srv/slate/build -v $(pwd)/source:/srv/slate/source slate
