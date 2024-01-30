FROM nextcloud:latest

COPY entrypoint.sh /
RUN chmod 775 /entrypoint.sh

ENTRYPOINT [ "/entrypoint.sh" ]
CMD ["apache2-foreground"]