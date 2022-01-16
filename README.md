# complaintsAnaysis
Analysis of complaints
- personal information issue to upload
- using amounts of 48 files 
# Description
- complaints analysis is displayed by wordcloud
- 11 parts is here
- make wordcloud by quater, parts(question, request, suggest)
# Characteristic
- wordcloud by python
- language : python
- tool : Google colab
# Quick view
{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "name": "sound_arparking.ipynb",
      "provenance": [],
      "collapsed_sections": [],
      "mount_file_id": "1QE_11nX3-usgygzu14bmMPvMs1Kk_cF3",
      "authorship_tag": "ABX9TyPqwh3ItUkee4ETcDD9OL1n"
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "code",
      "metadata": {
        "id": "4qHf0nxK02YU"
      },
      "source": [
        "pip install konlpy"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "1VKSV-wOiBqj"
      },
      "source": [
        "import pandas as pd\n",
        "import numpy as np\n",
        "from konlpy.tag import Okt\n",
        "from wordcloud import WordCloud, ImageColorGenerator, STOPWORDS\n",
        "import matplotlib.pyplot as plt\n",
        "%matplotlib inline\n",
        "okt = Okt()\n",
        "import matplotlib.font_manager as fm\n",
        "import re\n",
        "from PIL import Image\n",
        "from io import BytesIO \n",
        "import datetime\n",
        "from collections import Counter"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "FdywTozLiRit"
      },
      "source": [
        "labels = ['place','date','messenger','category','type','due','summary','name','phone','email','detail','receive','address','end','period','address_detail','result','result_detail','sign','etc']\n",
        "data_arp = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/sounds/sounds_place_arparking.csv', names = labels, encoding='cp949')\n",
        "data_arp.head()"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "RiejVyxnPopP"
      },
      "source": [
        "circle_mask = np.array(Image.open('/content/drive/MyDrive/Colab Notebooks/circle_img.jpg'))"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "LH8zQq2aL9ql"
      },
      "source": [
        "arp_detail = data_arp['detail']\n",
        "arp_d_tolist = arp_detail.values.tolist()\n",
        "arp_d_list = ''\n",
        "for i in arp_d_tolist:\n",
        "  arp_d_list += i\n",
        "arp_d_nouns = okt.nouns(arp_d_list)\n",
        "arp_d_n = ''\n",
        "for i in arp_d_nouns:\n",
        "  arp_d_n += i+' '\n",
        "arp_d_nouns_count = Counter(arp_d_nouns)\n",
        "stopwords = set(STOPWORDS)\n",
        "stopwords.update(['주차장','아름동'])"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "cE31WDpYMcDI"
      },
      "source": [
        "wd_arp_d = WordCloud(max_font_size=200,background_color=\"white\",mask=circle_mask,font_path='/content/drive/MyDrive/Colab Notebooks/sounds/malgun.ttf',stopwords=stopwords).generate(arp_d_n)\n",
        "fig = plt.figure()\n",
        "plt.imshow(wd_arp_d, interpolation='bilinear')\n",
        "plt.axis('off')\n",
        "wd_arp_d.to_file(filename='/content/drive/MyDrive/Colab Notebooks/wordcloud_img/wd_arp_d.jpg')"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "GpdBl10EtRzr"
      },
      "source": [
        "arp_question = data_arp[data_arp['type'] == \"질의\"]\n",
        "arp_question_detail = arp_question['detail']\n",
        "\n",
        "arp_check = data_arp[data_arp['type'] == \"확인\"]\n",
        "arp_check_detail = arp_check['detail']\n",
        "\n",
        "arp_request = data_arp[data_arp['type'] == \"건의\"]\n",
        "arp_request_detail = arp_request['detail']"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "HlnVffZVMNx9"
      },
      "source": [
        "질의"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "hguVNBbpeFnC"
      },
      "source": [
        "arp_qd_tolist = arp_question_detail.values.tolist()\n",
        "arp_qd_list = ''\n",
        "for i in arp_qd_tolist:\n",
        "  arp_qd_list += i"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "sO-G4dTvIKST"
      },
      "source": [
        "arp_qd_nouns = okt.nouns(arp_qd_list)\n",
        "arp_qd_n = ''\n",
        "for i in arp_qd_nouns:\n",
        "  arp_qd_n += i+' '"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "Oo0dyXx7qqY5"
      },
      "source": [
        "arp_qd_nouns_count = Counter(arp_qd_nouns)\n",
        "arp_qd_nouns_count"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "vN35SalkMVKu"
      },
      "source": [
        "stopwords = set(STOPWORDS)\n",
        "# stopwords.update(['모집', '임대', '아파트', '행복'])"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "itbGy5cuGAUQ"
      },
      "source": [
        "wd_arp_qd = WordCloud(max_font_size=250,background_color=\"white\",mask=circle_mask,font_path='/content/drive/MyDrive/Colab Notebooks/sounds/malgun.ttf',stopwords=stopwords).generate(arp_qd_n)\n",
        "fig = plt.figure()\n",
        "plt.imshow(wd_arp_qd, interpolation='bilinear')\n",
        "plt.axis('off')\n",
        "wd_arp_qd.to_file(filename='/content/drive/MyDrive/Colab Notebooks/wordcloud_img/wd_arp_qd.jpg')"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "0c13DBGVMSEU"
      },
      "source": [
        "확인(=0)"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "HcJj1SkmMSEU"
      },
      "source": [
        "arp_cd_tolist = arp_check_detail.values.tolist()\n",
        "arp_cd_list = ''\n",
        "for i in arp_cd_tolist:\n",
        "  arp_cd_list += i"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "iGb_OXMcMSEV"
      },
      "source": [
        "arp_cd_nouns = okt.nouns(arp_cd_list)\n",
        "arp_cd_n = ''\n",
        "for i in arp_cd_nouns:\n",
        "  arp_cd_n += i+' '"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "kOTBiSp-MSEV"
      },
      "source": [
        "arp_cd_nouns_count = Counter(arp_cd_nouns)\n",
        "arp_cd_nouns_count"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "kCFnjnbIMSEW"
      },
      "source": [
        "stopwords = set(STOPWORDS)\n",
        "# stopwords.update(['모집', '임대', '아파트', '행복'])"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "2V_p_6mTMSEW"
      },
      "source": [
        "wd_arp_cd = WordCloud(max_font_size=300,background_color=\"white\",mask=circle_mask,font_path='/content/drive/MyDrive/Colab Notebooks/sounds/malgun.ttf',stopwords=stopwords).generate(arp_cd_n)\n",
        "fig = plt.figure()\n",
        "plt.imshow(wd_arp_cd, interpolation='bilinear')\n",
        "plt.axis('off')\n",
        "wd_arp_cd.to_file(filename='/content/drive/MyDrive/Colab Notebooks/wordcloud_img/wd_arp_cd.jpg')"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "LyeGO-iJMURB"
      },
      "source": [
        "건의"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "cVcNFa7VMURB"
      },
      "source": [
        "arp_rd_tolist = arp_request_detail.values.tolist()\n",
        "arp_rd_list = ''\n",
        "for i in arp_rd_tolist:\n",
        "  arp_rd_list += i"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "4fBySnj2MURB"
      },
      "source": [
        "arp_rd_nouns = okt.nouns(arp_rd_list)\n",
        "arp_rd_n = ''\n",
        "for i in arp_rd_nouns:\n",
        "  arp_rd_n += i+' '"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "u-WgUH5LMURB"
      },
      "source": [
        "arp_rd_nouns_count = Counter(arp_rd_nouns)\n",
        "arp_rd_nouns_count"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "5SMCS2jaMURB"
      },
      "source": [
        "stopwords = set(STOPWORDS)\n",
        "stopwords.update(['주차장','아름동'])"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "SOA7P1S0MURC"
      },
      "source": [
        "wd_arp_rd = WordCloud(max_font_size=250,background_color=\"white\",mask=circle_mask,font_path='/content/drive/MyDrive/Colab Notebooks/sounds/malgun.ttf',stopwords=stopwords).generate(arp_rd_n)\n",
        "fig = plt.figure()\n",
        "plt.imshow(wd_arp_rd, interpolation='bilinear')\n",
        "plt.axis('off')\n",
        "wd_arp_rd.to_file(filename='/content/drive/MyDrive/Colab Notebooks/wordcloud_img/wd_arp_rd.jpg')"
      ],
      "execution_count": null,
      "outputs": []
    }
  ]
}
