ansible-role-cups_lpadmin
=============================

Role for manage printers in CUPS Printing System.

Example configuration
------------------------

## Global configuration:

```yaml
---
## Global
cups_lpadmin_mgmt: 'true'
cups_lpadmin_purge: 'true'
cups_lpadmin_ppd_source: '../../files/cups_lpadmin' # /roles/role -> ansible/files
cups_lpadmin_ipp_port: ':631'
cups_lpadmin_ipp_proto: 'ipp://'
cups_lpadmin_lpd_proto: 'lpd://'
cups_lpadmin_socket_proto: 'socket://'
cups_lpadmin_hp_net: 'hp:/net/'
cups_lpadmin_hp_usb: 'hp:/usb/'
cups_lpadmin_media: 'iso_a4_210x297mm'
cups_lpadmin_disable_snmp: 'snmp=false'

## HP P2055
cups_lpadmin_p2055_friendly_name: 'HP_P2055'
cups_lpadmin_p2055_driver: 'drv:///hp/hpcups.drv/hp-laserjet_p2055-pcl3.ppd'
cups_lpadmin_p2055_usb_name: 'HP_LaserJet_P2055?serial='
hp_p2055_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_ipp_proto'] + hostvars[inventory_hostname]['hp_p2055_address'] + hostvars[inventory_hostname]['cups_lpadmin_ipp_port'] + '/' + 'printers' + '/' + hostvars[inventory_hostname]['cups_lpadmin_p2055_friendly_name'] + '?' + hostvars[inventory_hostname]['cups_lpadmin_disable_snmp'] }}"
hp_p2055_usb: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_usb'] + hostvars[inventory_hostname]['cups_lpadmin_p2055_usb_name'] + hostvars[inventory_hostname]['hp_p2055_address'] }}"

## HP P2035
cups_lpadmin_p2035_friendly_name: 'HP_P2035'
cups_lpadmin_p2035_driver: 'drv:///hp/hpcups.drv/hp-laserjet_p2035-pcl3.ppd'
cups_lpadmin_p2035_usb_name: 'HP_LaserJet_P2035?serial='
hp_p2035_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_ipp_proto'] + hostvars[inventory_hostname]['hp_p2035_address'] + hostvars[inventory_hostname]['cups_lpadmin_ipp_port'] + '/' + 'printers' + '/' + hostvars[inventory_hostname]['cups_lpadmin_p2035_friendly_name'] + '?' + hostvars[inventory_hostname]['cups_lpadmin_disable_snmp'] }}"
hp_p2035_usb: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_usb'] + hostvars[inventory_hostname]['cups_lpadmin_p2035_usb_name'] + hostvars[inventory_hostname]['hp_p2035_address'] }}"

## HP M401dne
cups_lpadmin_m401_friendly_name: 'HP_M401'
cups_lpadmin_m401_driver: 'lsb/usr/HP/hp-laserjet_400_m401dne-ps.ppd.gz'
cups_lpadmin_m401_usb_name: 'HP_LaserJet_400_M401dne?serial='
cups_lpadmin_m401_net_name: 'HP_LaserJet_400_M401dne?ip='
hp_m401_ipp: "{{ hostvars[inventory_hostname]['cups_lpadmin_ipp_proto'] + hostvars[inventory_hostname]['hp_m401_address'] + hostvars[inventory_hostname]['cups_lpadmin_ipp_port'] + '/' + 'printers' + '/' + hostvars[inventory_hostname]['cups_lpadmin_m401_friendly_name'] + hostvars[inventory_hostname]['cups_lpadmin_disable_snmp'] }}"
hp_m401_usb: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_usb'] + hostvars[inventory_hostname]['cups_lpadmin_m401_usb_name'] + hostvars[inventory_hostname]['hp_m401_address'] }}"
hp_m401_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_net'] + hostvars[inventory_hostname]['cups_lpadmin_m401_net_name'] + hostvars[inventory_hostname]['hp_m401_address'] }}"

## HP M1536dnf
cups_lpadmin_m1536_friendly_name: 'HP_M1536'
cups_lpadmin_m1536_driver: 'drv:///hp/hpcups.drv/hp-laserjet_m1539dnf_mfp-pcl3.ppd'
cups_lpadmin_m1536_net_name: 'HP_LaserJet_M1536dnf_MFP?ip='
hp_m1536_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_net'] + hostvars[inventory_hostname]['cups_lpadmin_m1536_net_name'] + hostvars[inventory_hostname]['hp_m1536_address'] }}"

## HP M127fn
cups_lpadmin_m127_friendly_name: 'HP_M127'
cups_lpadmin_m127_driver: 'drv:///hp/hpcups.drv/hp-laserjet_pro_mfp_m127fn.ppd'
cups_lpadmin_m127_net_name: 'HP_LaserJet_Pro_MFP_M127fn?ip='
hp_m127_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_net'] + hostvars[inventory_hostname]['cups_lpadmin_m127_net_name'] + hostvars[inventory_hostname]['hp_m127_address'] }}"

## TSC TTP-245C
cups_lpadmin_ttp245_driver_4x1: 'tsc_ttp245c_4x1in.ppd'
cups_lpadmin_ttp245_driver_4x3: 'tsc_ttp245c_4x3in.ppd'
cups_lpadmin_ttp245_friendly_name_4x1: 'TTP-245C-4x1in'
cups_lpadmin_ttp245_friendly_name_4x3: 'TTP-245C-4x3in'
cups_lpadmin_ttp245_lpd_options: 'format=l&snmp=false'
cups_lpadmin_ttp245_socket_options: 'waiteof=false&snmp=false'
tsc_ttp245_net_4x1: "{{ hostvars[inventory_hostname]['cups_lpadmin_lpd_proto'] + hostvars[inventory_hostname]['tsc_ttp245_address'] + '/' + hostvars[inventory_hostname]['tsc_ttp245_queue_4x1'] + '?' + hostvars[inventory_hostname]['cups_lpadmin_ttp245_lpd_options'] }}"
tsc_ttp245_net_4x3: "{{ hostvars[inventory_hostname]['cups_lpadmin_lpd_proto'] + hostvars[inventory_hostname]['tsc_ttp245_address'] + '/' + hostvars[inventory_hostname]['tsc_ttp245_queue_4x3'] + '?' + hostvars[inventory_hostname]['cups_lpadmin_ttp245_lpd_options'] }}"

```

## Group/host configuration:

**HP M1536dnf MFP, via ethernet example**

```yaml
---
hp_m1536_address: "192.168.1.1"

cups_lpadmin:
  - name: "{{ hostvars[inventory_hostname]['cups_lpadmin_m1536_friendly_name'] }}"
    uri: "{{ hp_m1536_net }}"
    model: "{{ hostvars[inventory_hostname]['cups_lpadmin_m1536_driver'] }}"
    options:
      media: "{{ hostvars[inventory_hostname]['cups_lpadmin_media'] }}"
```

**HP P2055, via IPP example**

```yaml
---
hp_p2055_transport: "{{ hp_p2055_net }}"
hp_p2055_address: "192.168.1.1" # another CUPS instance with shared HP_P2055

cups_lpadmin:
  - name: "{{ hostvars[inventory_hostname]['cups_lpadmin_p2055_friendly_name'] }}"
    uri: "{{ hp_p2055_transport }}"
    options:
      media: "{{ hostvars[inventory_hostname]['cups_lpadmin_media'] }}"
```

**HP P2055, via USB example**

```yaml
---
hp_p2055_address: 'S1728P7' # take address via lsusb or lsusb.py
hp_p2055_transport: "{{ hp_p2055_usb }}"

cups_lpadmin:
  - name: "{{ hostvars[inventory_hostname]['cups_lpadmin_p2055_friendly_name'] }}"
    uri: "{{ hp_p2055_transport }}"
    model: "{{ hostvars[inventory_hostname]['cups_lpadmin_p2055_driver'] }}"
    default: "true"
    shared: "true"
    options:
      media: "{{ hostvars[inventory_hostname]['cups_lpadmin_media'] }}"
```

**TSC TTP-245C, via LPD example**

```yaml
---
tsc_ttp245_address: '192.168.128.213'
tsc_ttp245_queue_4x1: "TSC5"

cups_lpadmin:
  - name: "{{ hostvars[inventory_hostname]['cups_lpadmin_ttp245_friendly_name_4x1'] }}"
    driver: "ppd"
    uri: "{{ tsc_ttp245_net_4x1 }}"
    model: "{{ hostvars[inventory_hostname]['cups_lpadmin_ttp245_driver_4x1'] }}"
```
