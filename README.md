# Geocoding API

[![Build](https://github.com/open-meteo/geocoding-api/actions/workflows/test.yml/badge.svg)](https://github.com/open-meteo/geocoding-api/actions/workflows/test.yml)

Todo:
- Reconsider using protobuf library for json encoding (faster, but skips empty values, https://github.com/apple/swift-protobuf/issues/1171)
- include additional postal database http://download.geonames.org/export/zip/
- correctly implement iso2 county code filter
- GeoIP support + weighted results by distance
- Coordinates proximity search


## Installation on ubuntu 20.04
The standalone `geocodingapi` binary can run on any 64-bit linux with recent libc. Currently only basic installation instructions for ubuntu 20.04 are available. Later Docker and others can be provided.

```bash
api install zip

wget https://github.com/open-meteo/geocoding-api/releases/download/0.0.6/geocoding-api_0.0.6_focal_amd64.deb
dpkg -i geocoding-api_0.0.6_focal_amd64.deb

mkdir /var/lib/geocoding-api/data
cd /var/lib/geocoding-api/data
mkdir zip
curl http://download.geonames.org/export/dump/allCountries.zip -o allCountries.zip
curl http://download.geonames.org/export/dump/alternateNames.zip -o alternateNames.zip
curl http://download.geonames.org/export/zip/allCountries.zip -o zip/allCountries.zip
unzip allCountries.zip
unzip alternateNames.zip
cd zip; unzip allCountries.zip; cd ..

systemctl enable geocoding-api.service
systemctl start geocoding-api.service
systemctl status geocoding-api.service
```

Additionally, nginx proxy should be used

## Terms & Privacy
Open-Meteo APIs are free for open-source developer and non-commercial use. We do not restrict access, but ask for fair use.

If your application exceeds 10'000 requests per day, please contact us. We reserve the right to block applications and IP addresses that misuse our service.

For commercial use of Open-Meteo APIs, please contact us.

All data is provided as is without any warranty.

We do not collect any personal data. We do not share any personal information. We do not integrate any third party analytics, ads, beacons or plugins.

## Data License
API data are offered under Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)

You are free to share: copy and redistribute the material in any medium or format and adapt: remix, transform, and build upon the material.

Attribution: You must give appropriate credit, provide a link to the license, and indicate if changes were made. You may do so in any reasonable manner, but not in any way that suggests the licensor endorses you or your use.

You must include a link next to any location, Open-Meteo data are displayed like:

<a href="https://open-meteo.com/">Weather data by Open-Meteo.com</a>

NonCommercial: You may not use the material for commercial purposes.


## Source Code License
Open-Meteo is open-source under the GNU Affero General Public License Version 3 (AGPLv3) or any later version. You can [find the license here](LICENSE). Exceptions are third party source-code with individual licensing in each file.
