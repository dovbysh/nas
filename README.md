## minidlna

```bash
docker run -e PUID=1000 -e PGID=1000 -d --restart=unless-stopped --name minidlna \
  --net=host \
  -v /mnt/sdb1/video:/media \
  -e MINIDLNA_MEDIA_DIR=/media \
  -e MINIDLNA_FRIENDLY_NAME=aK53SMmini \
  vladgh/minidlna
```

## qbittorrent-nox
```bash
QBT_LEGAL_NOTICE=confirm   QBT_VERSION=latest \         
  QBT_TORRENTING_PORT=6881 \
  QBT_WEBUI_PORT=8080 \
  QBT_CONFIG_PATH=/home/dovbysh/qbtorrent_config \
  QBT_DOWNLOADS_PATH=/mnt/sdb1/video docker run \
  -d -t --restart=unless-stopped \
  --name qbittorrent-nox \
  --read-only \
  \
  --stop-timeout 1800 \
  --tmpfs /tmp \
  -e QBT_LEGAL_NOTICE \
  -e QBT_TORRENTING_PORT \
  -e QBT_WEBUI_PORT \
  -p "$QBT_TORRENTING_PORT":"$QBT_TORRENTING_PORT"/tcp \
  -p "$QBT_TORRENTING_PORT":"$QBT_TORRENTING_PORT"/udp \
  -p "$QBT_WEBUI_PORT":"$QBT_WEBUI_PORT"/tcp \
  -v "$QBT_CONFIG_PATH":/config \
  -v "$QBT_DOWNLOADS_PATH":/downloads \
  qbittorrentofficial/qbittorrent-nox:${QBT_VERSION}
```
