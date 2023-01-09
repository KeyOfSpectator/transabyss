From centos:centos7
LABEL maintainer="KeyOfSpectator <fsc606@163.com>"

WORKDIR /workspace/transabyss
ADD . /workspace/transabyss

RUN yum install -y python36
RUN yum install -y python3-devel

# yum update
# RUN mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
# RUN curl "http://mirrors.aliyun.com/repo/Centos-7.repo" -o /etc/yum.repos.d/CentOS-Base.repo
# RUN yum makecache

RUN yum install -y wget

# cmake > 3.16
RUN wget https://github.com/Kitware/CMake/releases/download/v3.25.1/cmake-3.25.1-linux-x86_64.tar.gz
RUN tar zxvf cmake-3.25.1-linux-x86_64.tar.gz



RUN ln -s /workspace/transabyss/cmake-3.25.1-linux-x86_64/bin/cmake /usr/bin/cmake
RUN yum groupinstall -y "Development Tools"

RUN cmake --version

# RUN yum install -y cmake
# RUN yum install -y g++
RUN pip-3.6 install python-igraph==0.9.11


# RUN wget 'https://repo.anaconda.com/miniconda/Miniconda3-py310_22.11.1-1-Linux-x86_64.sh'
# RUN chmod 755 ./*.sh
# RUN ./Miniconda3-py310_22.11.1-1-Linux-x86_64.sh -b -p $HOME/miniconda

# refer https://stackoverflow.com/questions/49714499/skip-installing-confirmyes-or-no-in-dockerfile
# this is a very big file, about 700+MB
RUN wget 'https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh'
RUN chmod 755 ./*.sh
RUN /bin/bash ./Anaconda3-2022.10-Linux-x86_64.sh -u -b -p /opt/conda
RUN ln -s /opt/conda/bin/conda  /usr/bin/conda 
RUN ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh 
RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc 
RUN echo "conda activate base" >> ~/.bashrc 

# RUN yum install -y conda
RUN conda create -y -n abyss-env
RUN source /etc/profile.d/conda.sh
RUN conda activate abyss-env
RUN conda install -c bioconda -y abyss

RUN rm -rf /usr/bin/python
RUN ln -s /usr/bin/python3.6 /usr/bin/python
#RUN export PATH=$PATH:/workspace/transabyss/

RUN echo "export PATH=/usr/bin:/workspace/transabyss:$PATH" >> ~/.bashrc

#ENTRYPOINT ["transabyss"]

