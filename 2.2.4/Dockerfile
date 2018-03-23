FROM dogbull/centos-python
MAINTAINER ParkJooHyeon <www.jrr.kr@gmail.com>


ENV \
    GDAL_VERSION=2.2.4 \
    LD_LIBRARY_PATH="/usr/local/lib/:${LD_LIBRARY_PATH}" \
    CPLUS_INCLUDE_PATH="/usr/local/include/python3.6m/:${CPLUS_INCLUDE_PATH}"


RUN \
    yum install -y epel-release && \
    yum update -y && \
    yum install -y \
        geos-devel \
        proj-devel \
        hdf5-devel \
        netcdf-devel \
        libgeotiff-devel \
        libjpeg-turbo-devel \
        libpng-devel \
        giflib-devel \
        postgresql-devel && \
    yum clean all


RUN \
    mkdir /tmp/workspace/ && \
    cd /tmp/workspace/ && \
    curl -O http://download.osgeo.org/gdal/${GDAL_VERSION}/gdal-${GDAL_VERSION}.tar.gz && \
    tar xvfz gdal-${GDAL_VERSION}.tar.gz && \
    cd gdal-${GDAL_VERSION} && \
    ./configure --with-python=/usr/local/bin/python3.6m && \
    make && \
    make install && \
    echo "/usr/local/lib" > /etc/ld.so.conf.d/gdal.conf  && \
    ldconfig && \
    cd swig/python && \
    make install && \
    cd / && \
    rm -rf /tmp/workspace/
