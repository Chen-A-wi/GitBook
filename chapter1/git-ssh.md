# 生成Git SSH

---

* ## Mac

  * Step1:

    首先開啟你的終端機輸入`ssh-keygen`。

  * Step2:  
    壓Enter鍵，終端機會請你輸入兩次密碼\(不想設密碼可以直接壓Enter\)。

  * Step3:  
    輸入`cat .ssh/id_rsa.pub`之後燒等下就會印出ssh金鑰了。

  最後再將它加入GitHub還是GitLab就結束了，即可使用sourceTree或是其他平台來同步專案你開發的專案嘍！

* ## Windows

  * Step1:

    首先去下載[Git](https://gitforwindows.org/)。

  * Step2:

    開啟你的終端機輸入`ssh-keygen`。

  * Step3:

    壓Enter鍵，終端機會請你輸入兩次密碼\(不想設密碼可以直接壓Enter\)。

  * Step4:

    接著去`c:\\使用者\(你的用戶名稱)\.ssh`，用記事本開啟`id_rsa.pub`就可以複製貼上喽!



