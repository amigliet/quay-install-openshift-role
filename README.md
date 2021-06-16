# quay-install-openshift-role

Ansible role to install Red Hat Quay Operator on OpenShift.

## Requirements
This role requires Kubernetes Collection which can be installed via Ansible Galaxy CLI:
```
ansible-galaxy collection install community.kubernetes
```

## Role Variables
For default variables see [defaults/main.yaml](defaults/main.yaml).

### Generic variables
| Variable                                          | Default      |
| :------------------------------------------------ | :----------: |
| quay_install_openshift_role_feat_anonymous_access | True         |
| quay_install_openshift_role_registry_title        | Red Hat Quay |
| quay_install_openshift_role_registry_title_short  | Red Hat Quay |
| quay_install_openshift_role_super_users           | -            |

### Authentication variables
| Variable                                        | Default  |
| :---------------------------------------------- | :------: |
| quay_install_openshift_role_authentication_type | Database |
| quay_install_openshift_role_feat_team_syncing   | false    |
| quay_install_openshift_role_ldap_admin_dn       | -        |
| quay_install_openshift_role_ldap_admin_passwd   | -        |
| quay_install_openshift_role_ldap_base_dn        | -        |
| quay_install_openshift_role_ldap_email_attr     | mail     |
| quay_install_openshift_role_ldap_uid_attr       | uid      |
| quay_install_openshift_role_ldap_uri            | -        |
| quay_install_openshift_role_ldap_user_filter    | -        |
| quay_install_openshift_role_ldap_user_rdn       | -        |

Usage example for LDAP identity provider:
```
  vars:
    quay_install_openshift_role_authentication_type: LDAP
    quay_install_openshift_role_ldap_admin_dn: uid=quay,ou=users,ou=employees,dc=my,dc=domain,dc=com
    quay_install_openshift_role_ldap_admin_passwd: supersecret1234
    quay_install_openshift_role_ldap_base_dn:
      - dc=my
      - dc=domain
      - dc=com
    quay_install_openshift_role_ldap_email_attr: mail
    quay_install_openshift_role_ldap_uid_attr: uid
    quay_install_openshift_role_ldap_uri: ldap://ldapserver.my.domain.com
    quay_install_openshift_role_ldap_user_filter: (someOtherField=someOtherValue)
    quay_install_openshift_role_ldap_user_rdn:
      - ou=users
      - ou=employees
```

### Storage variables
| Variable                                        | Default | Choices       |
| :---------------------------------------------- | :-----: | :-----------: |
| quay_install_openshift_role_s3_backend          | -       | GCS, AWS, RGW |
| quay_install_openshift_role_s3_access_key       | -       | -             |
| quay_install_openshift_role_s3_bucket_name      | -       | -             |
| quay_install_openshift_role_s3_secret_key       | -       | -             |
| quay_install_openshift_role_s3_aws_host         | -       | -             |
| quay_install_openshift_role_s3_rgw_hostname     | -       | -             |
| quay_install_openshift_role_s3_rgw_port         | -       | -             |
| quay_install_openshift_role_proxy_storage       | True    | True, False   |
| quay_install_openshift_role_storage_replication | False   | True, False   |

AWS usage example:
```
  vars:
    quay_install_openshift_role_cr_objectstorage: false
    quay_install_openshift_role_cr_configBundleSecret: true
    quay_install_openshift_role_s3_aws_host: <aws_host>
    quay_install_openshift_role_s3_backend: "AWS"
    quay_install_openshift_role_s3_access_key: <access_key>
    quay_install_openshift_role_s3_bucket_name: bucket01
    quay_install_openshift_role_s3_secret_key: <secret_key>
```

GCS usage example:
```
  vars:
    quay_install_openshift_role_cr_objectstorage: false
    quay_install_openshift_role_cr_configBundleSecret: true
    quay_install_openshift_role_s3_backend: "GCS"
    quay_install_openshift_role_s3_access_key: <access_key>
    quay_install_openshift_role_s3_bucket_name: bucket01
    quay_install_openshift_role_s3_secret_key: <secret_key>
```

RADOS Gateway usage example:
```
  vars:
    quay_install_openshift_role_cr_objectstorage: false
    quay_install_openshift_role_cr_configBundleSecret: true
    quay_install_openshift_role_s3_backend: "RGW"
    quay_install_openshift_role_s3_access_key: <access_key>
    quay_install_openshift_role_s3_bucket_name: bucket01
    quay_install_openshift_role_s3_secret_key: <secret_key>
    quay_install_openshift_role_s3_rgw_hostname: 192.168.0.5:9001
```

### TLS Certificates variables
| Variable                                            | Default  |
| :-------------------------------------------------- | :------: |
| quay_install_openshift_role_extra_ca_cert_custom_ca | -        |
| quay_install_openshift_role_server_hostname         | -        |
| quay_install_openshift_role_ssl_cert                | -        |
| quay_install_openshift_role_ssl_key                 | -        |

Usage example:
```
  vars:
    quay_install_openshift_role_server_hostname: quay.apps.mycluster.mydomain.com
    quay_install_openshift_role_ssl_cert: "{{ lookup('file', 'mycert.crt') }}"
    quay_install_openshift_role_ssl_key: "{{ lookup('file', 'mycert.key') }}"
    quay_install_openshift_role_extra_ca_cert_custom_ca: "{{ lookup('file', 'ca-bundle.crt') }}"
```

The definition of these variables will automatically configure:
```
apiVersion: quay.redhat.com/v1
kind: QuayRegistry
metadata:
[...]
spec:
  components:
[...]
    - kind: route
      managed: False
[...]
```

## Dependencies
None.

## Example Playbook
```
---
- hosts: localhost
  gather_facts: no

  tasks:

    - import_role:
        name: quay-install-openshift-role
...
```
