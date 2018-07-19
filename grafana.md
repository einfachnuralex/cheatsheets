#

# docker

docker run \
  -d \
  -p 3000:3000 \
  --name=grafana \
  -e "GF_SERVER_ROOT_URL=http://grafana.fritz.box" \
  -e "GF_SECURITY_ADMIN_PASSWORD=secret" \
  grafana/grafana
