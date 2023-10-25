# sc_update_kev_query
Update an Tenable.sc query based on  known exploitable vulnerabilites from CISA

## Install

```
# clone repository into current folder
$ git clone https://github.com/agroome/sc_update_kev_query.git

# change to project folder
$ cd sc_update_kev_query
 
# create and activate a virtual environment
$ python3 -m venv ./venv
$ source ./venv/bin/activate

# install requirements into venv
(venv)$ pip install -r requirements.txt
```

After installing create a file called .env in the project folder with your SC api keys:
```
SC_ACCESS_KEY=your_access_key
SC_SECRET_KEY=your_secret_key
```

Edit update_known_exploited.py and ensure these values reflect the IP and port of your Tenable.sc installation:
```
sc_host = '127.0.0.1'
sc_port = 443
```

## Running

### running from the CLI
```
# cd into the project folder and activate your virtual environment
$ cd sc_update_kev_query
$ source venv/bin/activate
(venv)$ python ./update_known_exploited.py
```

### running from cron
If you need to run from a cron job (without actiating the venv), you can specify the full path to the python executable in your virtual env along with the full path to the script file.
 
/path_to_location/sc_update_kev_query/venv/bin/python /path_to_location/sc_update_kev_query/update_known_exploited.py

## Known Issues
The first time the filter is created they query fails due likely due to a bug in pytenable. After the first run, 
 - edit the query by copying the filter values (the list of cves)
 - delete the filter from the query
 - add a new filter to the query for cveID and paste in the cve values
 - save the query

Subsequent runs should result in a successful query.