# cups_lpadmin

Role for manage printers in CUPS Printing System.

## Requirements

* Ansible 2.8+;

## Extra

* ppd storage is madatory setting if you will use external ppd's:
  * `file`: ppd's is a files on deployment host:

  ```yaml
  cups_lpadmin:
  - ppd_storage:
    - storage_type: 'file'
      # /roles/role -> ansible/files
      storage_source: '../../files/cups_lpadmin'
  ```

  * `s3`: ppd's source is a Amazon S3 bucket:

  ```yaml
  cups_lpadmin:
  - ppd_storage:
    - storage_type: 's3'
      storage_source:
  # AWS access key id. If not set then the value of the AWS_ACCESS_KEY
  # environment variable is used.
      - aws_access_key: "{{ aws_s3_access_key }}"
  # AWS secret key. If not set then the value of the AWS_SECRET_KEY environment
  # variable is used.
        aws_secret_key: "{{ aws_s3_secret_key }}"
  # Bucket name.
        bucket: "{{ aws_s3_bucket }}"
  # Time limit (in seconds) for the URL generated and returned by S3.
        expiration: '120'
  # Enable fakeS3.
        rgw: "{{ aws_s3_rgw }}"
  # S3 URL endpoint for usage with fakeS3. Otherwise assumes AWS.
        s3_url: "{{ aws_s3_url }}"
  # When set to 'no', SSL certificates will not be validated.
        validate_certs: "{{ omit }}"
  # S3 region.
        region: "{{ omit }}"
  # Use this boto profile.
        profile: "{{ omit }}"
  # Prefix ('folder') where objects placed in bucket, i.e.:
  # s3://ansible/ansible-role-cups_lpadmin/*.ppd
        object_prefix: 'ansible-role-cups_lpadmin'
  ```

## Example configuration
#### Global configuration:

```yaml
---
cups_lpadmin:
# Install packages or not.
- install_package: 'true'
# Purge all printers before deploy or not.
  purge_printers: 'true'
  settings: "{{ cups_lpadmin_settings }}"
  ppd_storage:
  - storage_type: 's3'
    storage_source:
    - aws_access_key: "{{ aws_s3_access_key }}"
      aws_secret_key: "{{ aws_s3_secret_key }}"
      bucket: 'ansible'
      expiration: '120'
      object_prefix: 'ansible-role-cups_lpadmin'

cups_lpadmin_ipp_port: ':631'
cups_lpadmin_ipp_proto: 'ipp://'
cups_lpadmin_lpd_proto: 'lpd://'
cups_lpadmin_socket_proto: 'socket://'
cups_lpadmin_hp_net: 'hp:/net/'
cups_lpadmin_hp_usb: 'hp:/usb/'
cups_lpadmin_tsc_lpd_options: 'format=l&snmp=false'
cups_lpadmin_tsc_socket_options: 'waiteof=false&snmp=false'
cups_lpadmin_ricoh_options: 'waiteof=false&waitprinter=false'
cups_lpadmin_media: 'iso_a4_210x297mm'
cups_lpadmin_disable_snmp: 'snmp=false'

## HP M127fs (grayscale, 1-sided printing)
cups_lpadmin_m127_friendly_name: 'HP_M127'
cups_lpadmin_m127_driver: 'drv:///hp/hpcups.drv/hp-laserjet_pro_mfp_m127fs.ppd'
cups_lpadmin_m127_net_name: 'HP_LaserJet_Pro_MFP_M127fs?ip='
# Ethernet, hp proto
hp_m127_net: "{{
  cups_lpadmin_hp_net + cups_lpadmin_m127_net_name + hp_m127_address }}"

## HP M225rdn (grayscale, 2-sided printing)
cups_lpadmin_m225_friendly_name: 'HP_M225'
cups_lpadmin_m225_driver:
  'drv:///hp/hpcups.drv/hp-laserjet_pro_mfp_m225_m226-pcl3.ppd'
cups_lpadmin_m225_net_name: 'HP_LaserJet_Pro_MFP_M225rdn?ip='
# Ethernet, hp proto
hp_m225_net: "{{
  cups_lpadmin_hp_net + cups_lpadmin_m225_net_name + hp_m225_address }}"

## HP M227sdn
cups_lpadmin_m227_friendly_name: 'HP_M227'
cups_lpadmin_m227_driver: 'drv:///hp/hpcups.drv/hp-laserjet_pro_mfp_m227sdn.ppd'
cups_lpadmin_m227_net_name: 'HP_LaserJet_Pro_MFP_M227sdn?ip='
hp_m227_net: "{{
  cups_lpadmin_hp_net + cups_lpadmin_m227_net_name + hp_m227_address }}"

## HP M401dne (grayscale, 2-sided printing)
cups_lpadmin_m401_friendly_name: 'HP_M401'
cups_lpadmin_m401_driver: 'lsb/usr/HP/hp-laserjet_400_m401dne-ps.ppd.gz'
cups_lpadmin_m401_usb_name: 'HP_LaserJet_400_M401dne?serial='
cups_lpadmin_m401_net_name: 'HP_LaserJet_400_M401dne?ip='
# Ethernet, ipp proto
hp_m401_ipp: "{{ cups_lpadmin_ipp_proto + hp_m401_address +
  cups_lpadmin_ipp_port + '/' + 'printers' + '/' +
  cups_lpadmin_m401_friendly_name + cups_lpadmin_disable_snmp }}"
# USB
hp_m401_usb: "{{
  cups_lpadmin_hp_usb + cups_lpadmin_m401_usb_name + hp_m401_address }}"
# Ethernet, hp proto
hp_m401_net: "{{
  cups_lpadmin_hp_net + cups_lpadmin_m401_net_name + hp_m401_address }}"

## HP M402dn / M402dne (grayscale, 2-sided printing)
cups_lpadmin_m402d_friendly_name: 'HP_M402'
cups_lpadmin_m402d_driver:
  'drv:///hp/hpcups.drv/hp-laserjet_m402d-m403d-pcl3.ppd'
cups_lpadmin_m402d_net_name: 'HP_LaserJet_M402dn?ip='
# Ethernet, hp proto
hp_m402d_net: "{{
  cups_lpadmin_hp_net + cups_lpadmin_m402d_net_name + hp_m402d_address }}"

## HP M402n (grayscale, 1-sided printing)
cups_lpadmin_m402_friendly_name: 'HP_M402'
cups_lpadmin_m402_driver:
  'drv:///hp/hpcups.drv/hp-laserjet_m402d-m403d-pcl3.ppd'
cups_lpadmin_m402_net_name: 'HP_LaserJet_M402n?ip='
# Ethernet, hp proto
hp_m402_net: "{{
  cups_lpadmin_hp_net + cups_lpadmin_m402_net_name + hp_m402_address }}"

## HP M426fdn (grayscale, 2-sided printing)
cups_lpadmin_m426_friendly_name: 'HP_M426'
cups_lpadmin_m426_driver:
  'drv:///hp/hpcups.drv/hp-laserjet_mfp_m426-m427-pcl3.ppd'
cups_lpadmin_m426_net_name: 'HP_LaserJet_MFP_M426fdn?ip='
# Ethernet, hp proto
hp_m426_net: "{{
  cups_lpadmin_hp_net + cups_lpadmin_m426_net_name + hp_m426_address }}"

## HP M1536dnf (grayscale, 2-sided printing)
cups_lpadmin_m1536_friendly_name: 'HP_M1536'
cups_lpadmin_m1536_driver:
  'drv:///hp/hpcups.drv/hp-laserjet_m1539dnf_mfp-pcl3.ppd'
cups_lpadmin_m1536_net_name: 'HP_LaserJet_M1536dnf_MFP?ip='
hp_m1536_net: "{{
  cups_lpadmin_hp_net + cups_lpadmin_m1536_net_name + hp_m1536_address }}"

## HP P2035
cups_lpadmin_p2035_friendly_name: 'HP_P2035'
cups_lpadmin_p2035_driver: 'drv:///hp/hpcups.drv/hp-laserjet_p2035-pcl3.ppd'
cups_lpadmin_p2035_usb_name: 'HP_LaserJet_P2035?serial='
# Ethernet, ipp proto
hp_p2035_net: "{{ cups_lpadmin_ipp_proto + hp_p2035_address +
  cups_lpadmin_ipp_port + '/' + 'printers' + '/' +
  cups_lpadmin_p2035_friendly_name + '?' + cups_lpadmin_disable_snmp }}"
# USB
hp_p2035_usb: "{{
  cups_lpadmin_hp_usb + cups_lpadmin_p2035_usb_name + hp_p2035_address }}"

## HP P2055
cups_lpadmin_p2055_friendly_name: 'HP_P2055'
cups_lpadmin_p2055_driver: 'drv:///hp/hpcups.drv/hp-laserjet_p2055-pcl3.ppd'
cups_lpadmin_p2055_usb_name: 'HP_LaserJet_P2055?serial='
# Ethernet, ipp proto
hp_p2055_net: "{{ cups_lpadmin_ipp_proto + hp_p2055_address +
  cups_lpadmin_ipp_port + '/' + 'printers' + '/' +
  cups_lpadmin_p2055_friendly_name + '?' + cups_lpadmin_disable_snmp }}"
# USB
hp_p2055_usb: "{{
  cups_lpadmin_hp_usb + cups_lpadmin_p2055_usb_name + hp_p2055_address }}"

## TSC TC200
cups_lpadmin_tc200_driver_4x1: 'tsc_tc200_4x1in.ppd'
cups_lpadmin_tc200_driver_4x3: 'tsc_tc200_4x3in.ppd'
cups_lpadmin_tc200_friendly_name_4x1: 'TC200-4x1in'
cups_lpadmin_tc200_friendly_name_4x3: 'TC200-4x3in'
# 4" x 1" stickers
tsc_tc200_net_4x1: "{{ cups_lpadmin_lpd_proto + tsc_tc200_address + '/' +
  tsc_tc200_queue_4x1 + '?' + cups_lpadmin_tsc_lpd_options }}"
# 4" x 3" stickers
tsc_tc200_net_4x3: "{{ cups_lpadmin_lpd_proto + tsc_tc200_address + '/' +
  tsc_tc200_queue_4x3 + '?' + cups_lpadmin_tsc_lpd_options }}"

## TSC TTP-245C
cups_lpadmin_ttp245_driver_4x1: 'tsc_ttp245c_4x1in.ppd'
cups_lpadmin_ttp245_driver_4x3: 'tsc_ttp245c_4x3in.ppd'
cups_lpadmin_ttp245_friendly_name_4x1: 'TTP-245C-4x1in'
cups_lpadmin_ttp245_friendly_name_4x3: 'TTP-245C-4x3in'
# 4" x 1" stickers
tsc_ttp245_net_4x1: "{{ cups_lpadmin_lpd_proto + tsc_ttp245_address + '/' +
  tsc_ttp245_queue_4x1 + '?' + cups_lpadmin_tsc_lpd_options }}"
# 4" x 3" stickers
tsc_ttp245_net_4x3: "{{ cups_lpadmin_lpd_proto + tsc_ttp245_address + '/' +
  tsc_ttp245_queue_4x3 + '?' + cups_lpadmin_tsc_lpd_options }}"
```

#### Group/host configuration:

###### HP M1536dnf MFP, via ethernet example

```yaml
---
hp_m1536_address: '192.168.1.1'

cups_lpadmin_settings:
- name: "{{ cups_lpadmin_m1536_friendly_name }}"
  uri: "{{ hp_m1536_net }}"
  model: "{{ cups_lpadmin_m1536_driver }}"
  options:
    media: "{{ cups_lpadmin_media }}"
```

###### HP P2055, via IPP example

```yaml
---
hp_p2055_address: '192.168.1.1' # another CUPS instance with shared HP_P2055

cups_lpadmin_settings:
- name: "{{ cups_lpadmin_p2055_friendly_name }}"
  uri: "{{ hp_p2055_net }}"
  model: 'raw'
  default: 'true'
```

###### HP P2055, via USB example

```yaml
---
hp_p2055_address: 'S1728P7' # take address via lsusb or lsusb.py

cups_lpadmin_settings:
- name: "{{ cups_lpadmin_p2055_friendly_name }}"
  uri: "{{ hp_p2055_usb }}"
  model: "{{ cups_lpadmin_p2055_driver }}"
  default: 'true'
  shared: 'true'
  options:
    media: "{{ cups_lpadmin_media }}"
```

###### TSC TTP-245C, via LPD example

```yaml
---
tsc_ttp245_address: '192.168.1.1'
tsc_ttp245_queue_4x1: 'TSC5'

cups_lpadmin_settings:
- name: "{{ cups_lpadmin_ttp245_friendly_name_4x1 }}"
  driver: 'ppd'
  uri: "{{ tsc_ttp245_net_4x1 }}"
  model: "{{ cups_lpadmin_ttp245_driver_4x1 }}"
```
