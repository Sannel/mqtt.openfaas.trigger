ARG tag=2.2
FROM mcr.microsoft.com/dotnet/core/runtime:${tag} AS base
WORKDIR /app
COPY  qemu-aarch64-static /usr/bin/
COPY MQTT.OpenFaas.Trigger/ .
RUN ln -s  /var/run/secrets/kubernetes.io/serviceaccount/ca.crt /etc/ssl/certs/kubernetes.pem \
    && groupadd -g 1200 house \
    && useradd -m house -g house -u 1100 \
    && chown -R house:house /app \
    && rm -f /usr/bin/qemu-aarch64-static
USER house
ENTRYPOINT ["dotnet", "MQTT.OpenFaas.Trigger.dll"]