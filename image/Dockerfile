# Copyright (c) 2017 Software AG, Darmstadt, Germany and/or its licensors
#
# Licensed under the Apache License, Version 2.0 (the "License"); you may not use this 
# file except in compliance with the License. You may obtain a copy of the License at
# http://www.apache.org/licenses/LICENSE-2.0
# Unless required by applicable law or agreed to in writing, software distributed under the
# License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, 
# either express or implied. 
# See the License for the specific language governing permissions and limitations under the License.
#
# This Dockerfile creates an image that can run Apama components, and is built
# from an existing Apama installation. The build should be run from the root
# of your Software AG installation. e.g. '/opt/softwareag/'

# Pull CentOS 7 base image from the Docker Hub - this is the latest supported
# operating system for this version of Apama.
FROM centos:7

MAINTAINER SoftwareAG

# Copy and customize the minimal contents from the installation in order to
# run non-interactive Apama components
COPY ./common/security/ /common/security/
COPY ./jvm/jvm/ /java_home/
COPY ./Apama/adapters/ /apama_home/adapters/
COPY ./Apama/bin/ /apama_home/bin/
COPY ./Apama/lib/ /apama_home/lib/
COPY ./Apama/third_party/ /apama_home/third_party/
COPY ./Apama/monitors/ /apama_home/monitors/
COPY ./Apama/etc /apama_home/etc/

# Set the environment appropriate to running Apama executables
ENV PATH=/apama_home/bin/:/java_home/bin:/apama_home/third_party/apache_ant/bin:$PATH\
    LD_LIBRARY_PATH=/apama_home/lib/:/apama_home/adapters/lib/:/java_home/jre/lib/amd64/server/:/java_home/jre/lib/amd64/:/apama_home/third_party/python/lib:/apama_work/lib/\
    APAMA_HOME=/apama_home/\
    APAMA_WORK=/apama_work/\
    APAMA_JRE=/java_home/jre/\
    ANT_HOME=/apama_home/third_party/apache_ant

# Expose the default server port for the correlator, IAF, dashboard server management, dashboard server data, display server management and
# display server data respectively
EXPOSE 15903 16903 28888 3278 28889 3279

# This is the current working directory, and also the location that the
# (default CMD) correlator obtains the licence file from; license/license.txt,
# the same location in a typically installed apama-work.
WORKDIR /apama_work/

# The default operation for the image is to start a correlator, but this can
# be overridden by the command given to 'docker run'
CMD ["correlator", "-j"]
