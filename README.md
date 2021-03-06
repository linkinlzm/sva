# Repo for SVA_Fall2017 Final Project
# ---Attention: this repo contains malicious files!---
## How to generate the key
```
openssl genrsa -out private.pem 2048
openssl rsa -in private.pem -outform PEM -pubout -out public.pem
```

## How to run
- To encrypt the files:
```
sudo ./upx64 encrypt public.pem
```
- To decrypt the files:
You need to download a new repo before decryption.
```
sudo ./upx64 private.pem
```
- Fine all encrypted files
```
sudo find / -name '*encrypted'
```
## How to recover the files
- Find all encrypted files
```
./sort_files.sh ./encfiles/ > sorted_list
```
- Get some enc-file paths for next step
```
head -3 sorted_list
```
- How to find the seed for decryption
<p>The script will parse the modification time of the directory. Then it will brute force to find the IV for decryption.</p>

```
python decrypter.py -f ./encfiles/.wireshark/recent_common.encrypted
```
<p>The output should be [*] Seed: 1512259893</p>

- To decrypt the files
```
python decrypter.py -s 1512259893 -l sorted_list -e error_list
```
