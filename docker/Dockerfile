FROM centos:7

COPY gotty /usr/local/bin/gotty
COPY startgotty /usr/local/bin/startgotty

RUN yum update -y \
  && yum install -y git curl vim nano tmux \
  && yum clean all -y \
  && cd /tmp \
  && curl -o oc.tar.gz https://mirror.openshift.com/pub/openshift-v3/clients/3.11.123/linux/oc.tar.gz \
  && tar -zxf oc.tar.gz \
  && mv oc /usr/local/bin/ \
  && rm -f oc.tar.gz \
  && useradd -m -u 1001 -g 0 user \
  && chown -R 0 /etc/passwd /home/user \
  && chmod -R g=u /etc/passwd /home/user \
  && echo "user:openshift" | chpasswd

USER 1001
WORKDIR /home/user

CMD ["/usr/local/bin/startgotty"]
EXPOSE 8080