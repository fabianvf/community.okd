FROM registry.access.redhat.com/ubi8/ubi

ENV OPERATOR=/usr/local/bin/ansible-operator \
    USER_UID=1001 \
    USER_NAME=ansible-operator\
    HOME=/opt/ansible \
    ANSIBLE_LOCAL_TMP=/opt/ansible/tmp

RUN yum install -y \
      glibc-langpack-en \
      git \
      make \
      python3 \
      python3-devel \
      python3-pip \
      python3-setuptools \
 && pip3 install --no-cache-dir --upgrade setuptools pip \
 && pip3 install --no-cache-dir \
      openshift \
      ansible \
      molecule \
  && yum clean all \
  && rm -rf $HOME/.cache

COPY . /opt/ansible

WORKDIR /opt/ansible

RUN echo "${USER_NAME}:x:${USER_UID}:0:${USER_NAME} user:${HOME}:/sbin/nologin" >> /etc/passwd \
 && mkdir -p "${HOME}/.ansible/tmp" \
 && chown -R "${USER_UID}:0" "${HOME}" \
 && chmod -R ug+rwX "${HOME}" \
 && mkdir /go \
 && chown -R "${USER_UID}:0" /go \
 && chmod -R ug+rwX /go


USER ${USER_UID}
