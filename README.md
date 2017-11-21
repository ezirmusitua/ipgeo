## Proxy Geo Detector 
[![](https://travis-ci.org/ezirmusitua/ipgeo.svg?branch=master)](https://travis-ci.org/ezirmusitua/ipgeo)[![PyPI](https://img.shields.io/pypi/dm/getIpGeoInfo.svg)](https://pypi.python.org/pypi?%3Aaction=pkg_edit&name=getIpGeoInfo)[![Coverage Status](https://coveralls.io/repos/github/ezirmusitua/ipgeo/badge.svg?branch=master)](https://coveralls.io/github/ezirmusitua/ipgeo?branch=master)[![codebeat badge](https://codebeat.co/badges/67f9663f-af34-4615-9c9b-b52411200c76)](https://codebeat.co/projects/github-com-ezirmusitua-ipgeo-master)  
get ip address's geographic information  
### Features  
1. get ip address's geographic information  
2. use exporter to export with specific format  

### Requirements  
1. [geoip2](https://github.com/maxmind/GeoIP2-python)    
2. [Maxmind Geo Database](http://dev.maxmind.com/geoip/geoip2/geolite2/)    

### Installation  
```bash    
pip install -U getIpGeoInfo  
cd project/
curl -O http://geolite.maxmind.com/download/geoip/database/GeoLite2-City.tar.gz  
tar -zxvf GeoLite2-City.tar.gz
```  

### Usage  
```python  
import os  

from getIpGeoInfo import IpGeo  
ip_address = '128.101.101.101'
# load database and init ip geo  
ip_geo = IpGeo.open_reader(os.path.split(os.path.realpath(__file__))[0] + '/GeoLite2-City.mmdb')(ip_address)  
# fetch original geoip2 data  
print(ip_geo.country)   # same in geoip2
print(ip_geo.city)      # same in geoip2
print(ip_geo.location)  # same in geoip2
print(ip_geo.postal)    # same in geoip2  
# get name with locale(default is en-US)  
print(ip_geo.country_name)  
print(ip_geo.city_name)  
# get location label, default format is `country, city`, you can assign template like `{country}|{city}`  
print(ip_geo.location_label())
print(ip_geo.location_label(tmpl='{country}|{city}')  
# get position info, default format is `({latitude}, {longitude})`, you can assign template like `{latitude}, {longitude}`  
print(ip_geo.position())
print(ip_geo.position(tmpl='{latitude}, {longitude}')  
# get zip code  
print(ip_geo.zip_code)
print(ip_geo.postal_code())  
# export with exporter  
## use default json exporter  
print(ip_geo.export())  
## use customize exporter  
def address_exporter(_ip_geo):
    return _ip_geo.location_label() + ': ' + _ip_geo.zip_code
print(ip_geo.export(address_exporter))
```  

### Todos 
 - [ ] Use mock instead file load in tests.py

### License  
[MIT license](https://opensource.org/licenses/MIT)  
### Acknowledgment  
**This product includes GeoLite2 data created by MaxMind, available from [http://www.maxmind.com](http://www.maxmind.com)**    

