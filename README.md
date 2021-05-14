# quay-install-openshift-role

## Variables
### Default variables
```
# Red Hat Quay Operator Subscription variables
quay_install_openshift_role_channel_version: v3.5
quay_install_openshift_role_csv_version: v3.5.1

# Quay namespace
quay_install_openshift_role_namespace: quay-registry
#quay_install_openshift_role_nodeselector: ""

# Quay CR
quay_install_openshift_role_cr_instance_name: instance
quay_install_openshift_role_cr_clair: true
quay_install_openshift_role_cr_horizontalpodautoscaler: true
quay_install_openshift_role_cr_mirror: true
quay_install_openshift_role_cr_monitoring: true
quay_install_openshift_role_cr_objectstorage: true
quay_install_openshift_role_cr_postgres: true
quay_install_openshift_role_cr_redis: true
quay_install_openshift_role_cr_route: true
quay_install_openshift_role_cr_configBundleSecret: false
quay_install_openshift_role_configBundleSecret_name: "instance-quay-config-bundle-000ff"
```

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
| quay_install_openshift_role_s3_rgw_port         | 443     | -             |
| quay_install_openshift_role_proxy_storage       | True    | True, False   |
| quay_install_openshift_role_storage_replication | False   | True, False   |

