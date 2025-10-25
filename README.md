[Exportação (1).ipynb](https://github.com/user-attachments/files/23137223/Exportacao.1.ipynb)# 1ª SPRINT

BACKLOG PARCIAL

[BACKLOG.docx](https://github.com/user-attachments/files/23110853/BACKLOG.docx)



MAPA MENTAL

<img width="561" height="660" alt="image" src="https://github.com/user-attachments/assets/676af997-9311-4ccf-bc20-e63da85e5c23" />



FLUXOGRAMA

<img width="901" height="696" alt="image" src="https://github.com/user-attachments/assets/23650ba5-b66c-47bf-ab91-36830d048052" />



DIAGRAMA DE GANTT(CRONOGRAMA)

<img width="1083" height="723" alt="image" src="https://github.com/user-attachments/assets/a7ae0dd1-b664-4cf9-874b-3e23bddeb961" />



FILTRAGEM DE DADOS PARCIAL PELO COLLAB(PHYTON)

[Uploading Expor{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": []
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
      "execution_count": null,
      "metadata": {
        "id": "GFAb-NLW34ag"
      },
      "outputs": [],
      "source": [
        "import pandas as pd"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "from google.colab import drive"
      ],
      "metadata": {
        "id": "_61HQpJB0-mT"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "drive.mount('/content/drive')"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "IWyKT5CE1JKr",
        "outputId": "f21d897e-0c06-40bd-fc5e-91bcb07e1f70"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Mounted at /content/drive\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "origem = '/content/drive/My Drive/Data/'"
      ],
      "metadata": {
        "id": "NRCWDn5y1kLc"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "arquivo_5 = origem + 'EXP_2025_MUN.csv'\n",
        "arquivo_4 = origem + 'EXP_2024_MUN.csv'\n",
        "arquivo_3 = origem + 'EXP_2023_MUN.csv'\n",
        "arquivo_2 = origem + 'EXP_2022_MUN.csv'\n",
        "arquivo_1 = origem + 'EXP_2021_MUN.csv'\n",
        "UF_MUN = origem + 'UF_MUN.csv'\n",
        "PAIS = origem + 'PAIS.csv'"
      ],
      "metadata": {
        "id": "qoO43HAc2OMS"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "Exp25mun = pd.read_csv(arquivo_1,low_memory=False,sep=';',encoding='UTF-8')\n",
        "Exp24mun = pd.read_csv(arquivo_2,low_memory=False,sep=';',encoding='UTF-8')\n",
        "Exp23mun = pd.read_csv(arquivo_3,low_memory=False,sep=';',encoding='UTF-8')\n",
        "Exp22mun = pd.read_csv(arquivo_4,low_memory=False,sep=';',encoding='UTF-8')\n",
        "Exp21mun = pd.read_csv(arquivo_5,low_memory=False,sep=';',encoding='UTF-8')\n",
        "ExpPais = pd.read_csv(PAIS,low_memory=False,sep=';',encoding='latin1')\n",
        "ExpUfmun = pd.read_csv(UF_MUN,low_memory=False,sep=';',encoding='latin1')"
      ],
      "metadata": {
        "id": "am2i1lXw21cM"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "exp_final = pd.concat([Exp24mun,Exp25mun,Exp23mun,Exp22mun,Exp21mun], ignore_index=True)"
      ],
      "metadata": {
        "id": "H_uP0VfHlama"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "exp_final = exp_final.merge(ExpPais[['CO_PAIS' , 'NO_PAIS']],on='CO_PAIS',how='left')"
      ],
      "metadata": {
        "id": "EE6RaXHZnrL5"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "exp_final = exp_final.merge(ExpUfmun[['CO_MUN_GEO' , 'NO_MUN']],left_on='CO_MUN', right_on='CO_MUN_GEO',how='left')"
      ],
      "metadata": {
        "id": "Xn8Gjyi0oe1K"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "exp_final = exp_final[exp_final['SG_UF_MUN'].str.startswith('SP')]"
      ],
      "metadata": {
        "id": "C7cAlHlRq6no"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "exp_final = exp_final[exp_final['NO_MUN'].isin(['SAO JOSE DOS CAMPOS' , 'JACAREI' , 'TAUBATE' , 'CACAPAVA'])]"
      ],
      "metadata": {
        "id": "_aTZZS9krqrQ"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "exp_final.to_csv(origem + 'Exportação_Dados.csv', index=False)"
      ],
      "metadata": {
        "id": "17crcLPfs3Dh"
      },
      "execution_count": null,
      "outputs": []
    }
  ]
}tação (1).ipynb…]()


Dados extraídos do Comex Stat, unificados em uma pasta do google drive, depois foi exportado para o Google Collab. Foi usado a linguagem Python e a biblioteca Pandas para realizar a filtragem de dados de acordo com o SH4 e as cidades do vale do paraíba, salvando em duas planilhas, uma para exportação e outra para importação.
[Dados Exportação e Importação.xlsm](https://github.com/user-attachments/files/23110682/Dados.Exportacao.e.Importacao.xlsm)



1° DASHBOARD

<img width="1310" height="738" alt="image" src="https://github.com/user-attachments/assets/0ab7853a-9b17-4ad3-aa1d-c692ec28b1d7" />



PLANO DE AÇÃO(5W2H)

<img width="1796" height="558" alt="image" src="https://github.com/user-attachments/assets/b51679d2-07fd-4ba1-890f-305e10c1f9a6" />



# 2ª SPRINT

BACKLOG

[backlog.xlsx](https://github.com/user-attachments/files/23111094/backlog.xlsx)


[userscore.xlsx](https://github.com/user-attachments/files/23111105/userscore.xlsx)



FILTRAGEM DE DADOS COMPLETA

[Dados completos.xlsm](https://github.com/user-attachments/files/23110984/Dados.completos.xlsm)

Foram adicionados todos códigos SH4 relacionados a nossa cadeia produtiva, para uma demonstração completa no nosso dashboard.
