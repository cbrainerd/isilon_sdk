## Installation
`pip install isilon_sdk_7_2`

or 

`pip install isilon_sdk_8_0`

## Example program

Here's an example of using the Python PAPI bindings to retrieve a list of NFS exports from your cluster:

```python
import isi_sdk_8_0 # or isi_sdk_7_2, depending on the release you downloaded
from isi_sdk_8_0.rest import ApiException
from pprint import pprint
import urllib3
urllib3.disable_warnings()

# configure username and password
isi_sdk_8_0.configuration.username = "YOUR_USERNAME"
isi_sdk_8_0.configuration.password = "YOUR_PASSWORD"
isi_sdk_8_0.configuration.verify_ssl = False

# configure host
host = "https://YOUR_CLUSTER_HOSTNAME_OR_NODE_IP_ADDRESS:8080"
api_client = isi_sdk_8_0.ApiClient(host)
protocols_api = isi_sdk_8_0.ProtocolsApi(api_client)

# get all exports
sort = "description"
limit = 50
dir = "ASC"
try: 
    api_response = protocols_api.list_nfs_exports(sort=sort, limit=limit, dir=dir)
    pprint(api_response)
except ApiException as e:
    print "Exception when calling ProtocolsApi->list_nfs_exports: %s\n" % e
```

There are more examples of coding to the Python PAPI bindings in the `tests/` subdirectory of this repo.  The tests currently run against a generic isi_sdk import which is how the bindings library is named by default if you build your own bindings.  If you want to run the tests against one of the libraries you've downloaded from the prebuilt releases page, you should change the `import isi_sdk` lines to `import isi_sdk_7_2` or `import isi_sdk_8_0` depending on which one you downloaded.
