FROM base-common
MAINTAINER jiangwei "jiangwei07061625@163.com"
ENV SYDIR_DOWNLOAD=/home/download LUAJIT_LIB=/usr/local/luajit/lib LUAJIT_INC=/usr/local/luajit/include/luajit-2.0 CPPFLAGS="-I/usr/local/include -I/usr/local/zlib/include -I/usr/local/pcre/include" LDFLAGS="-L/usr/local/lib -L/usr/local/lib64 -L/usr/local/zlib/lib -L/usr/local/pcre/lib" PATH=$PATH:/usr/local/git/bin:/usr/local/bin
RUN echo "" >> /etc/profile && echo "export LUAJIT_LIB=/usr/local/luajit/lib" >> /etc/profile && echo "export LUAJIT_INC=/usr/local/luajit/include/luajit-2.0" >> /etc/profile && echo "export CPPFLAGS='-I/usr/local/include -I/usr/local/zlib/include -I/usr/local/pcre/include'" >> /etc/profile && echo "export LDFLAGS='-L/usr/local/lib -L/usr/local/lib64 -L/usr/local/zlib/lib -L/usr/local/pcre/lib'" >> /etc/profile && echo "export PATH=\$PATH:/usr/local/git/bin:/usr/local/bin" >> /etc/profile && source /etc/profile
WORKDIR $SYDIR_DOWNLOAD

# git
ARG GIT_USERNAME
ARG GIT_USEREMAIL
COPY ./resources/linux/git-2.10.2.tar.gz $SYDIR_DOWNLOAD/git-2.10.2.tar.gz
RUN yum -y remove git && mkdir /usr/local/git && tar -xzf git-2.10.2.tar.gz && cd git-2.10.2/ && ./configure --prefix=/usr/local/git && make all && make install && rm -rf git-2.10.2/ && rm -rf git-2.10.2.tar.gz && git config --global user.name "${GIT_USERNAME}" && git config --global user.email "${GIT_USEREMAIL}"

# pcre
COPY ./resources/linux/pcre-8.42.tar.gz $SYDIR_DOWNLOAD/pcre-8.42.tar.gz
RUN mkdir /usr/local/pcre && tar -zxvf pcre-8.42.tar.gz && cd pcre-8.42/ && ./configure --prefix=/usr/local/pcre && make && make install && echo "/usr/local/pcre/lib" >> /etc/ld.so.conf && ldconfig && rm -rf pcre-8.42/

# zlib
COPY ./resources/linux/zlib-1.2.11.tar.gz $SYDIR_DOWNLOAD/zlib-1.2.11.tar.gz
RUN mkdir /usr/local/zlib && tar -zxvf zlib-1.2.11.tar.gz && cd zlib-1.2.11/ && ./configure --prefix=/usr/local/zlib && make && make install && echo "/usr/local/zlib/lib" >> /etc/ld.so.conf && ldconfig && rm -rf zlib-1.2.11/

# openssl
COPY ./resources/linux/openssl-1.0.2p.tar.gz $SYDIR_DOWNLOAD/openssl-1.0.2p.tar.gz
RUN mkdir /usr/local/openssl && tar -zxvf openssl-1.0.2p.tar.gz && cd openssl-1.0.2p/ && ./config --prefix=/usr/local/openssl shared zlib && make && make install && echo "/usr/local/openssl/lib" >> /etc/ld.so.conf && ldconfig && rm -rf openssl-1.0.2p/ && ln -s /usr/local/openssl/bin/openssl /usr/bin/openssl && ln -s /usr/local/openssl/include/openssl /usr/include/openssl

# nghtt2
COPY ./resources/linux/nghttp2-1.26.0.tar.bz2 $SYDIR_DOWNLOAD/nghttp2-1.26.0.tar.bz2
RUN tar -xf nghttp2-1.26.0.tar.bz2 && mv nghttp2-1.26.0/ /usr/local/nghttp2 && cd /usr/local/nghttp2 && ./configure && make && make install && rm -rf nghttp2-1.26.0.tar.bz2