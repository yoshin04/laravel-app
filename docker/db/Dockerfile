FROM mysql:5.7.12
EXPOSE 3306
ENV MYSQL_DATABASE=sample
ENV MYSQL_ROOT_PASSWORD=root 
ENV MYSQL_USER=user 
ENV MYSQL_PASSWORD=password123
COPY my.cnf /etc/mysql/conf.d/my.cnf
CMD ["mysqld"]