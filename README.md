# cups_lpadmin

Role for manage printers in CUPS Printing System.

## Requirements

* Ansible 2.5+;

## Example configuration
#### Global configuration:

```yaml
---
# Allow to manage printers.
cups_lpadmin_mgmt: 'true'
# Purge all printers before deploy.
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
# Ethernet, ipp proto
hp_p2055_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_ipp_proto'] +
                  hostvars[inventory_hostname]['hp_p2055_address'] +
                  hostvars[inventory_hostname]['cups_lpadmin_ipp_port'] +
                  '/' + 'printers' + '/' +
                  hostvars[inventory_hostname]['cups_lpadmin_p2055_friendly_name']
                  + '?' +
                  hostvars[inventory_hostname]['cups_lpadmin_disable_snmp'] }}"
# USB
hp_p2055_usb: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_usb'] +
                  hostvars[inventory_hostname]['cups_lpadmin_p2055_usb_name'] +
                  hostvars[inventory_hostname]['hp_p2055_address'] }}"

## HP P2035
cups_lpadmin_p2035_friendly_name: 'HP_P2035'
cups_lpadmin_p2035_driver: 'drv:///hp/hpcups.drv/hp-laserjet_p2035-pcl3.ppd'
cups_lpadmin_p2035_usb_name: 'HP_LaserJet_P2035?serial='
# Ethernet, ipp proto
hp_p2035_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_ipp_proto'] +
                  hostvars[inventory_hostname]['hp_p2035_address'] +
                  hostvars[inventory_hostname]['cups_lpadmin_ipp_port'] +
                  '/' + 'printers' + '/' +
                  hostvars[inventory_hostname]['cups_lpadmin_p2035_friendly_name']
                  + '?' +
                  hostvars[inventory_hostname]['cups_lpadmin_disable_snmp'] }}"
# USB
hp_p2035_usb: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_usb'] +
                  hostvars[inventory_hostname]['cups_lpadmin_p2035_usb_name'] +
                  hostvars[inventory_hostname]['hp_p2035_address'] }}"

## HP M225rdn (grayscale, 2-sided printing)
cups_lpadmin_m225_friendly_name: 'HP_M225'
cups_lpadmin_m225_driver: 'drv:///hp/hpcups.drv/hp-laserjet_pro_mfp_m225_m226-pcl3.ppd'
cups_lpadmin_m225_net_name: 'HP_LaserJet_Pro_MFP_M225rdn?ip='
# Ethernet, hp proto
hp_m225_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_net'] +
                 hostvars[inventory_hostname]['cups_lpadmin_m225_net_name'] +
                 hostvars[inventory_hostname]['hp_m225_address'] }}"

## HP M401dne (grayscale, 2-sided printing)
cups_lpadmin_m401_friendly_name: 'HP_M401'
cups_lpadmin_m401_driver: 'lsb/usr/HP/hp-laserjet_400_m401dne-ps.ppd.gz'
cups_lpadmin_m401_usb_name: 'HP_LaserJet_400_M401dne?serial='
cups_lpadmin_m401_net_name: 'HP_LaserJet_400_M401dne?ip='
# Ethernet, ipp proto
hp_m401_ipp: "{{ hostvars[inventory_hostname]['cups_lpadmin_ipp_proto'] +
                 hostvars[inventory_hostname]['hp_m401_address'] +
                 hostvars[inventory_hostname]['cups_lpadmin_ipp_port'] +
                 '/' + 'printers' + '/' +
                 hostvars[inventory_hostname]['cups_lpadmin_m401_friendly_name']
                 + hostvars[inventory_hostname]['cups_lpadmin_disable_snmp'] }}"
# USB
hp_m401_usb: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_usb'] +
                 hostvars[inventory_hostname]['cups_lpadmin_m401_usb_name'] +
                 hostvars[inventory_hostname]['hp_m401_address'] }}"
# Ethernet, hp proto
hp_m401_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_net'] +
                 hostvars[inventory_hostname]['cups_lpadmin_m401_net_name'] +
                 hostvars[inventory_hostname]['hp_m401_address'] }}"

## HP M402n (grayscale, 1-sided printing)
cups_lpadmin_m402_friendly_name: 'HP_M402'
cups_lpadmin_m402_driver: 'drv:///hp/hpcups.drv/hp-laserjet_m402d-m403d-pcl3.ppd'
cups_lpadmin_m402_net_name: 'HP_LaserJet_M402n?ip='
# Ethernet, hp proto
hp_m402_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_net'] +
                 hostvars[inventory_hostname]['cups_lpadmin_m402_net_name'] +
                 hostvars[inventory_hostname]['hp_m402_address'] }}"

## HP M402dn / M402dne (grayscale, 2-sided printing)
cups_lpadmin_m402d_friendly_name: 'HP_M402'
cups_lpadmin_m402d_driver: 'drv:///hp/hpcups.drv/hp-laserjet_m402d-m403d-pcl3.ppd'
cups_lpadmin_m402d_net_name: 'HP_LaserJet_M402dn?ip='
# Ethernet, hp proto
hp_m402d_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_net'] +
                  hostvars[inventory_hostname]['cups_lpadmin_m402d_net_name'] +
                  hostvars[inventory_hostname]['hp_m402d_address'] }}"

## HP M1536dnf (grayscale, 2-sided printing)
cups_lpadmin_m1536_friendly_name: 'HP_M1536'
cups_lpadmin_m1536_driver: 'drv:///hp/hpcups.drv/hp-laserjet_m1539dnf_mfp-pcl3.ppd'
cups_lpadmin_m1536_net_name: 'HP_LaserJet_M1536dnf_MFP?ip='
hp_m1536_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_net'] +
                  hostvars[inventory_hostname]['cups_lpadmin_m1536_net_name'] +
                  hostvars[inventory_hostname]['hp_m1536_address'] }}"

## HP M127fs (grayscale, 1-sided printing)
cups_lpadmin_m127_friendly_name: 'HP_M127'
cups_lpadmin_m127_driver: 'drv:///hp/hpcups.drv/hp-laserjet_pro_mfp_m127fs.ppd'
cups_lpadmin_m127_net_name: 'HP_LaserJet_Pro_MFP_M127fs?ip='
# Ethernet, hp proto
hp_m127_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_net'] +
                 hostvars[inventory_hostname]['cups_lpadmin_m127_net_name'] +
                 hostvars[inventory_hostname]['hp_m127_address'] }}"

## HP M227sdn
cups_lpadmin_m227_friendly_name: 'HP_M227'
cups_lpadmin_m227_driver: 'drv:///hp/hpcups.drv/hp-laserjet_pro_mfp_m227sdn.ppd'
cups_lpadmin_m227_net_name: 'HP_LaserJet_Pro_MFP_M227sdn?ip='
hp_m227_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_net'] +
                 hostvars[inventory_hostname]['cups_lpadmin_m227_net_name'] +
                 hostvars[inventory_hostname]['hp_m227_address'] }}"

## HP M426fdn (grayscale, 2-sided printing)
cups_lpadmin_m426_friendly_name: 'HP_M426'
cups_lpadmin_m426_driver: 'drv:///hp/hpcups.drv/hp-laserjet_mfp_m426-m427-pcl3.ppd'
cups_lpadmin_m426_net_name: 'HP_LaserJet_MFP_M426fdn?ip='
# Ethernet, hp proto
hp_m426_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_hp_net'] +
                 hostvars[inventory_hostname]['cups_lpadmin_m426_net_name'] +
                 hostvars[inventory_hostname]['hp_m426_address'] }}"

## Ricoh SP 3610SF
cups_lpadmin_sp3610_friendly_name: 'RICOH_SP3610SF'
cups_lpadmin_sp3610_driver: 'Ricoh-SP_3610SF-Postscript-Ricoh.ppd'
ricoh_sp3610_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_socket_proto'] +
                      hostvars[inventory_hostname]['ricoh_sp3610_address']
                      + '?' +
                      hostvars[inventory_hostname]['cups_lpadmin_ricoh_options'] }}"

## Ricoh SP 450DN
cups_lpadmin_sp450_friendly_name: 'RICOH_SP450DN'
cups_lpadmin_sp450_driver: 'Ricoh-SP_450DN-Postscript-Ricoh.ppd'
ricoh_sp450_net: "{{ hostvars[inventory_hostname]['cups_lpadmin_socket_proto'] +
                     hostvars[inventory_hostname]['ricoh_sp450_address'] + '?' +
                     hostvars[inventory_hostname]['cups_lpadmin_ricoh_options'] }}"

## TSC TTP-245C
cups_lpadmin_ttp245_driver_4x1: 'tsc_ttp245c_4x1in.ppd'
cups_lpadmin_ttp245_driver_4x3: 'tsc_ttp245c_4x3in.ppd'
cups_lpadmin_ttp245_friendly_name_4x1: 'TTP-245C-4x1in'
cups_lpadmin_ttp245_friendly_name_4x3: 'TTP-245C-4x3in'
# 4" x 1" stickers
tsc_ttp245_net_4x1: "{{ hostvars[inventory_hostname]['cups_lpadmin_lpd_proto'] +
                        hostvars[inventory_hostname]['tsc_ttp245_address'] +
                        '/' +
                        hostvars[inventory_hostname]['tsc_ttp245_queue_4x1'] +
                        '?' +
                        hostvars[inventory_hostname]['cups_lpadmin_tsc_lpd_options'] }}"
# 4" x 3" stickers
tsc_ttp245_net_4x3: "{{ hostvars[inventory_hostname]['cups_lpadmin_lpd_proto'] +
                        hostvars[inventory_hostname]['tsc_ttp245_address'] +
                        '/' +
                        hostvars[inventory_hostname]['tsc_ttp245_queue_4x3'] +
                        '?' +
                        hostvars[inventory_hostname]['cups_lpadmin_tsc_lpd_options'] }}"

## TSC TC200
cups_lpadmin_tc200_driver_4x1: 'tsc_tc200_4x1in.ppd'
cups_lpadmin_tc200_driver_4x3: 'tsc_tc200_4x3in.ppd'
cups_lpadmin_tc200_friendly_name_4x1: 'TC200-4x1in'
cups_lpadmin_tc200_friendly_name_4x3: 'TC200-4x3in'
# 4" x 1" stickers
tsc_tc200_net_4x1: "{{ hostvars[inventory_hostname]['cups_lpadmin_lpd_proto'] +
                       hostvars[inventory_hostname]['tsc_tc200_address'] + '/' +
                       hostvars[inventory_hostname]['tsc_tc200_queue_4x1'] +
                       '?' +
                       hostvars[inventory_hostname]['cups_lpadmin_tsc_lpd_options'] }}"
# 4" x 3" stickers
tsc_tc200_net_4x3: "{{ hostvars[inventory_hostname]['cups_lpadmin_lpd_proto'] +
                       hostvars[inventory_hostname]['tsc_tc200_address'] + '/' +
                       hostvars[inventory_hostname]['tsc_tc200_queue_4x3'] +
                       '?' +
                       hostvars[inventory_hostname]['cups_lpadmin_tsc_lpd_options'] }}"
```

#### Group/host configuration:

###### HP M1536dnf MFP, via ethernet example

```yaml
---
hp_m1536_address: '192.168.1.1'

cups_lpadmin:
  - name: "{{ hostvars[inventory_hostname]['cups_lpadmin_m1536_friendly_name'] }}"
    uri: "{{ hp_m1536_net }}"
    model: "{{ hostvars[inventory_hostname]['cups_lpadmin_m1536_driver'] }}"
    options:
      media: "{{ hostvars[inventory_hostname]['cups_lpadmin_media'] }}"
```

###### HP P2055, via IPP example

```yaml
---
hp_p2055_transport: "{{ hp_p2055_net }}"
hp_p2055_address: '192.168.1.1' # another CUPS instance with shared HP_P2055

cups_lpadmin:
  - name: "{{ hostvars[inventory_hostname]['cups_lpadmin_p2055_friendly_name'] }}"
    uri: "{{ hp_p2055_transport }}"
    options:
      media: "{{ hostvars[inventory_hostname]['cups_lpadmin_media'] }}"
```

###### HP P2055, via USB example

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

###### TSC TTP-245C, via LPD example

```yaml
---
tsc_ttp245_address: '192.168.128.213'
tsc_ttp245_queue_4x1: 'TSC5'

cups_lpadmin:
  - name: "{{ hostvars[inventory_hostname]['cups_lpadmin_ttp245_friendly_name_4x1'] }}"
    driver: "ppd"
    uri: "{{ tsc_ttp245_net_4x1 }}"
    model: "{{ hostvars[inventory_hostname]['cups_lpadmin_ttp245_driver_4x1'] }}"
```
