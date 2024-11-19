<p align="center"> ������������ ����������� ���������� ��������</p>
<p align="center">���������� �����������</p>
<p align="center">���������� ��������������� ����������� �����������</p>
<p align="center">������� ���</p>
<br><br><br><br><br><br><br>
<p align="center">������������ ������ �4</p>
<p align="center">�� ���������� ������ ������ ���������������� ������</p>
<p align="center">����: ������� � �������� "NIKA" (Intelligent Knowledge-driven Assistant)�</p>
<br><br><br><br><br>
<p align="right">��������:</p>
<p align="right">������� 2 �����</p>
<p align="right">������ ��-26</p>
<p align="right">������ �. �.</p>
<p align="right">���������:</p>
<p align="right">�������� �. �.</p>
<br><br><br><br><br>
<p align="center">����� 2024</p>

---

# ����� ������� #
1. ������� �����������.

2. ��������� ������ ������ �� ��������� ������ (�������� ������������ ���������, �������, ������� ������ � ��������� � �.�.). ������������������ ������ ������� �������������.

3. �������� ����� �� ����������� ������ � .md ������� (readme.md) � � ������� pull request ���������� ��� � ��������� ��������: trunk\ii0xxyy\task_04\doc.


---

# ���������� #

��������� Docker, � ��������� �� ����������� ������ NIKA, � ����� � ��������, � �������� ��������� ���� ������ � ���� ��������. ��� ��������� ������, ������ �� ����� ������������� � �������� ������ � ���� ��������.

Installation:
```
git clone -c core.longpaths=true -c core.autocrlf=true https://github.com/ostis-apps/nika
cd nika
git submodule update --init --recursive
docker compose pull
```
������:
```
docker compose up --no-build
```
��� ������� ����c���� 2 ���-����������:

sc-web: ```localhost:8000```

���-������ ����������������� ����������: ```localhost:3033```

sc-web:

![task041.png](task041.png)
![task043.png](task043.png)
![task046.png](task046.png)


Web-������ ����������������� ����������: 

![task042.png](task042.png)
![task044.png](task044.png)
![task045.png](task045.png)