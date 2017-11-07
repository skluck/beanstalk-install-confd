# Install confd on Elastic Beanstalk

This is an example of installing `jq` and `confd` as a part of `.ebextensions` in Elastic Beanstalk deployments.

See [.ebextensions/10-install-confd.config](.ebextensions/10-install-confd.config)

This config does the following:
- Install `jq` if not installed
- Install `confd` if not installed
- Install `confd_agent` service in `/etc/init.d` which Beanstalk can managed
- Add `confd.toml` config
    - Backend set to `ssm` by default (Note that `watch` does not currently work for `ssm`)
- Add `application.toml` application config which generates a json configuration file with values from `ssm`.
    - All configuration keys in the `/confd/$CONFD_APP_NAME/$CONFD_ENVIRONMENT` prefix are loaded. 

Requirements:
- Set `CONFD_APP_NAME`
- Set `CONFD_ENVIRONMENT`

TODO:
- Find a way to support ssm watching (cron?)
