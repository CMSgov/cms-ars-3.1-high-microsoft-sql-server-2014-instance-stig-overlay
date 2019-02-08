# cms-ars-3.1-high-microsoft-windows-2014-instance-stig-overlay

InSpec profile overlay to validate the secure configuration of Microsoft SQL Server 2014 Instance against [DISA's](https://iase.disa.mil/stigs/Pages/index.aspx) Microsoft SQL Server 2014 Instance STIG Version 1 Release 9 tailored for [CMS ARS 3.1](https://www.cms.gov/Research-Statistics-Data-and-Systems/CMS-Information-Technology/InformationSecurity/Info-Security-Library-Items/ARS-31-Publication.html) for CMS systems categorized as High.

## Getting Started  
It is intended and recommended that InSpec and this profile overlay be run from a __"runner"__ host (such as a DevOps orchestration server, an administrative management system, or a developer's workstation/laptop) against the target remotely over __winrm__.

__For the best security of the runner, always install on the runner the _latest version_ of InSpec and supporting Ruby language components.__ 

Latest versions and installation options are available at the [InSpec](http://inspec.io/) site.

The following attributes must be configured in an attributes file for the profile to run correctly. More information about InSpec attributes can be found in the [InSpec Profile Documentation](https://www.inspec.io/docs/reference/profiles/).

```
# Username for MSSQL DB Server
user: null

# Password for MSSQL DB Server
password: null

# Hostname for MSSQL DB Server
host: 'hostname'

# Instance name of the MSSQL DB Server
instance: 'MSSQL2014'

# Port of MSSQL DB Server
port: 1433

# Name of the specific database being evaluated within the MSSQL server
db_name: 'master'
```

## Running This Overlay
When the __"runner"__ host uses this profile overlay for the first time, follow these steps: 

```
mkdir profiles
cd profiles
git clone https://github.cms.gov/ispg/cms-ars-3.1-high-microsoft-sql-server-2014-instance-stig-overlay.git
git clone https://github.com/mitre/microsoft-sql-server-2014-instance-stig-baseline.git
cd cms-ars-3.1-high-microsoft-sql-server-2014-instance-stig-overlay
bundle install
cd ..
inspec exec cms-ars-3.1-high-microsoft-sql-server-2014-instance-stig-overlay --target=winrm://<your_target_host_name_or_ip_address> --user=<target_account_with_administrative_privileges> --password=<password_for_target_account> --reporter=cli json:<path_to_your_output_file/name_of_your_output_file.json> --attrs=cms-ars-3.1-high-microsoft-sql-server-2014-instance-stig-overlay/static-attributes.yml <path_to_your_attributes_file/name_of_your_attributes_file.yml>
```

For every successive run, follow these steps to always have the latest version of this overlay and dependent profiles:

```
cd profiles/microsoft-sql-server-2014-instance-stig-baseline
git pull
cd ../cms-ars-3.1-high-microsoft-sql-server-2014-instance-stig-overlay
git pull
bundle install
cd ..
inspec exec cms-ars-3.1-high-microsoft-sql-server-2014-instance-stig-overlay --target=winrm://<your_target_host_name_or_ip_address> --user=<target_account_with_administrative_privileges> --password=<password_for_target_account> --reporter=cli json:<path_to_your_output_file/name_of_your_output_file.json> --attrs=cms-ars-3.1-high-microsoft-sql-server-2014-instance-stig-overlay/static-attributes.yml <path_to_your_attributes_file/name_of_your_attributes_file.yml>
```

## Viewing the JSON Results

The JSON results output file can be loaded into __[heimdall-lite](https://mitre.github.io/heimdall-lite/)__ for a user-interactive, graphical view of the InSpec results. 

The JSON InSpec results file may also be loaded into a __[full heimdall server](https://github.com/mitre/heimdall)__, allowing for additional functionality such as to store and compare multiple profile runs.

## Authors
* Eugene Aronne
* Danny Haynes

## Special Thanks
* Aaron Lippold
* Alicia Sturtevant

## Getting Help
To report a bug or feature request, please open an [issue](https://github.cms.gov/ispg/cms-ars-3.1-high-microsoft-sql-server-2014-instance-stig-overlay/issues/new).

## License
This is licensed under the [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0) license. 

### NOTICE  

This software was produced for the U. S. Government under Contract Number HHSM-500-2012-00008I, and is subject to Federal Acquisition Regulation Clause 52.227-14, Rights in Data-General.  

No other use other than that granted to the U. S. Government, or to those acting on behalf of the U. S. Government under that Clause is authorized without the express written permission of The MITRE Corporation.

For further information, please contact The MITRE Corporation, Contracts Management Office, 7515 Colshire Drive, McLean, VA  22102-7539, (703) 983-6000.

### NOTICE
DISA STIGs are published by DISA IASE, see: https://iase.disa.mil/Pages/privacy_policy.aspx
