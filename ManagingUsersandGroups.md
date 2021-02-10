# Kullanıcıları ve Grupları Yönetme

Linux'un iki tür kullanıcısı vardır: insan ve sistem. Tüm kullanıcıların benzersiz kullanıcı tanımlamaları (UID) ve en az bir grup kimliği (GID) vardır. Tüm kullanıcıların, / etc / passwd altında listelenen grup olan bir birincil grubu vardır.



İnsan kullanıcıların kişisel dosyaları için kendi kişisel ev dizinleri vardır. Kullanıcı ana dizinleri / home dizinine aittir ve /home/ duchess'in sahibi olan örnek kullanıcımız Düşes gibi kullanıcı için adlandırılır. 

Kullanıcılar birden çok gruba ait olabilir ve ek grup üyeliklerine tamamlayıcı gruplar denir. Bir gruptaki kullanıcılar, o grubun tüm ayrıcalıklarına sahiptir.

Ayrıcalıklar, dosyalara ve komutlara erişimi kontrol eder ve sistem güvenliği için çok önemlidir.



Sistem kullanıcıları, sistem hizmetleri ve process'ler içindir. Sistem kullanıcıları, ayrıcalıklarını kontrol etmek için hesaplara ihtiyaç duyar ve 

```powershell
/home
```

 konumunda oturum açma bilgileri veya dizinleri yoktur.







