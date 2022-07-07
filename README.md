# ColddBox

Máquina virtual com sistema WordPress

![image](https://user-images.githubusercontent.com/56542755/177674926-a772c226-44cf-4a1e-a593-04844e117380.png)


## Ferramentas utilizadas:

- [Kali VM](https://kali.download/virtual-images/kali-2022.2/kali-linux-2022.2-virtualbox-amd64.ova)
  
  Máquina virtual com o Kali 

- [Virtual Box](https://www.virtualbox.org/wiki/Downloads)
 
	Utilizada para gerencias as VM's

- [ColddBox](https://www.vulnhub.com/entry/colddbox-easy,586/)

	VM explorada

## Setup

Configurei as VM's como descrito [aqui](https://medium.com/@gavinloughridge/a-beginners-guide-to-vulnhub-part-1-52b06466635d)

## Exploração

Comecei com o seguinte comando para ver as portas disponíveis

```
nmap -sV 10.10.10.2
```

que me retornou o seguinte, dizendo que a porta 80 estava disponível com http

![image](https://user-images.githubusercontent.com/56542755/177675513-f43503cf-1f6c-4cd7-bd3d-6ad7e03132a0.png)

com o seguinte comando pude ver os diretórios 

```
dirb http://10.10.10.2
```
![image](https://user-images.githubusercontent.com/56542755/177676069-68b0465f-9bfe-4415-92fe-8cf0b9d59fbf.png)

dentre os diretórios o **http://10.10.10.2/hidden/** me chamou a atenção, ao acessar ele pelo navegador aparece a seguinte mensagem

![image](https://user-images.githubusercontent.com/56542755/177676388-783043a4-cb0c-435a-aa2f-03a691b64f78.png)

com isso já se pode supor que o sistema tem ao menos o **Hugo** como usuário, e que o **c0ldd** pode ser outro com um grau mais alto de permissão (já que trocou a senha do Hugo). Então resolvi tentar pegar a senha do c0ldd por bruteforce com o **WpScan** com o seguinte comando

```
wpscan --url 10.10.10.2 -U c0ldd -P /usr/share/wordlists/rockyou.txt
```

como retorno obtive que a senha de c0ldd é **9876543210**

# Referências

- [A begginers guide to Vulnhub: part 1](https://medium.com/@gavinloughridge/a-beginners-guide-to-vulnhub-part-1-52b06466635d)
- [A begginers guide to Vulnhub: part 2](https://medium.com/@gavinloughridge/a-beginners-guide-to-vulnhub-part-2-b13c6314027c)
- [A begginers guide to Vulnhub: part 3](https://medium.com/@gavinloughridge/a-beginners-guide-to-vulnhub-part-3-bcf334d8cd04)
- [Kali wordslist](https://www.fosslinux.com/48115/kali-linux-wordlist-what-you-need-to-know.htm)
- [Use WPScan to scan WordPress for vulnerabilities on Kali](https://linuxconfig.org/use-wpscan-to-scan-wordpress-for-vulnerabilities-on-kali#:~:text=Vulnerabilities%20in%20WordPress%20can%20be,a%20website%20that's%20running%20WordPress.)
