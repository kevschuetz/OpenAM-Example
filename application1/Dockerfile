FROM httpd:2.4

# install web agent
RUN apt-get update && apt-get install -y wget unzip

RUN wget --show-progress --progress=bar:force:noscroll --quiet --output-document=/tmp/Apache_v24_Linux_64bit_4.1.1.zip https://github.com/OpenIdentityPlatform/OpenAM-Web-Agents/releases/download/4.1.1/Apache_v24_Linux_64bit_4.1.1.zip

RUN unzip /tmp/Apache_v24_Linux_64bit_4.1.1.zip -d /usr/

RUN rm /tmp/Apache_v24_Linux_64bit_4.1.1.zip

# password file
ENV PA_PASSWORD password
RUN echo $PA_PASSWORD > /tmp/pwd.txt
RUN cat /tmp/pwd.txt

# Copy custom configuration file to the container
COPY ./httpd.conf /usr/local/apache2/conf/httpd.conf

# Copy the HTML file to the webserver
#COPY ./index_old.html /usr/local/apache2/htdocs/index.html
COPY ./index.html /usr/local/apache2/htdocs/
RUN mkdir /usr/local/apache2/htdocs/admin
RUN mkdir /usr/local/apache2/htdocs/user
COPY ./admin_index.html /usr/local/apache2/htdocs/admin/index.html
COPY ./user_index.html /usr/local/apache2/htdocs/user/index.html

# Create apache user
RUN useradd apache

# install web agent
#RUN /usr/web_agents/apache24_agent/bin/agentadmin --s "/usr/local/apache2/conf/httpd.conf" "http://openam:8080/openam" "http://www.example.com:8081" "/" "apache_1" "/tmp/pwd.txt" --acceptLicence --changeOwner