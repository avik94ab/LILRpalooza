# LILRpalooza

A protype for an extreme simple API server that a user can
submit a LILR/LAIR sequence to get GFE annotation form 
https://feature.b12x.org

## build 
```
cd docker/
bash build.sh
```

## run
```
docker run -p 8080:8080 lilr_palooza
```

## test
```
cd server/tests
bash test1.sh
```

## issues
This is just from a couple of hours coding for the hackathon #dash16.
It has very limited testing and minimum error handling.


