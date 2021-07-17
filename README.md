# DockerPesa
DockerPesa is a complete M-Pesa API docker image, You dont need any SDK or programming language, 
all you need is two minutes deploy it 

## Installation
Just clone this repository into your local computer

```bash
git clone git@github.com:GraHms/dockerpesa.git
```
## Usage
edit the config.json file. 
M-Pesa API uses the same service provider code for testting, 
You can change the default 171717 code when you are in production

```json
{
    "api_key":"paste in here, your mpesa api key",
    "public_key":"paste in here your mpesa public key",
    "sp_code": "171717"
    
}
```
## Understanding the Dockerfile
This by default it exposes the port to 8080, 
but you can choose any port you want, by adding EXPOSE ${your port number}

```Dockerfile
FROM grahms/dockerpesa

COPY . ./
```
## Image Build
Go to the terminal and run your the dockerfile to build the image with your configurations

```bash
docker build --pull --rm -f "Dockerfile" -t mydockerpesa "."
```
## Run Image
Now you can run you can create a docker container by running the image you just created
```bash
docker run --rm -d  -p 8080:8080/tcp mydockerpesa:latest
```
## C2B Payments
### Request

`POST /c2b/`

    curl -i -H 'Accept: application/json' -d 'msidsdn=84xxxxxx&amount=300'  http://localhost:8080/c2b/
### Response
    
    https://developer.mpesa.vm.co.mz/apis/5/6/#response
    
## B2C Payments
### Request

`POST /b2c/`

    curl -i -H 'Accept: application/json' -d 'msidsdn=84xxxxxx&amount=300'  http://localhost:8080/b2c/
### Response
    
    https://developer.mpesa.vm.co.mz/apis/5/6/#response

## Query Transaction
### Request

`POST /query/`
     curl -i -H 'Accept: application/json' -d 'qr=QueryReference&tpr=thirdPartyReference'  http://localhost:8080/reverse/

    
### Response
    
    https://developer.mpesa.vm.co.mz/apis/5/6/#response
    
## Reverse Transaction
### Request

`POST /reverse/`
     curl -i -H 'Accept: application/json' -d 'tid=TransactionId&sc=securityCredential&ii=initiatorIdentifier&tpr=ThirdPartyReference' http://localhost:8080/reverse/
    
### Response
    
    https://developer.mpesa.vm.co.mz/apis/5/6/#response
    
    
  ## B2b Transaction
### Request

`POST /b2b/`
     curl -i -H 'Accept: application/json' -d 'rpc=RemotePartyCode&amount=200'  http://localhost:8080/b2b/

    
### Response
    
    https://developer.mpesa.vm.co.mz/apis/5/6/#response


## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT License](https://choosealicense.com/licenses/mit/)

Copyright (c) 2020 Ismael Antonio GraHms

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
