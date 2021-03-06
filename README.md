## Overview
This Docker image is Apache 2.4.6 with Shibboleth SP 3.1.0.-3.1 installed running on CentOS 7.

This image is based on the work previously done by https://www.github.com/Unicon/shibboleth-sp-dockerized

This image can be used as a base image overriding the configuration with local changes.

Ports 80 and 443 are exposed for traffic.

## Logs
Logs for httpd and shibd have been configured to output to the console so that Docker's logging facilities are supported. Each of these logs have been prefaced with an identifier that indicates the type of entry being outputted: `httpd-error`, `httpd-combined`, `sp-shibd`, `sp-native`, `sp-transaction`, `sp-sign`, etc.

## Use as a Base
This image is ideal for use as a base image for one's own deployment. 

For example, add your SP configurations to `./shibboleth-sp` and you app files to `./appfiles/`.

Next, assuming the Dockerfile is similar to this example:

```
FROM oapass/shibboleth-sp

ADD /shibboleth-sp/ /etc/shibboleth/
ADD /appfiles/ /var/www/html/ 
```

> This will take the base image that is available in the Docker repository and download it. Next, it overrides all of the base files with your local configuration.

The dependant image can be built by running:

```
docker build --tag="<org_id>/<image_name>" .
```

Now, just execute the new image:

```
$ docker run -dP --name="app-local-test" <org_id>/<image_name> 
```

## Building

From source:

```
$ docker build --tag="<org_id>/shibboleth-sp" github.com/oapass/shibboleth-sp-dockerized
```

## Author

  * John Gasper (<jgasper@unicon.net>)
  * Derek Belrose (<dbelrose@jhu.edu>)


## LICENSE

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
