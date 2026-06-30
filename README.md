[Practice.ipynb](https://github.com/user-attachments/files/29518850/Practice.ipynb)
# Test_repository_2
{
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
      "execution_count": 1,
      "metadata": {
        "id": "CCjkSORlDLZQ"
      },
      "outputs": [],
      "source": [
        "import requests\n",
        "BASE = \"https://clinicaltrials.gov/api/v2/studies\"\n",
        "\n",
        "def run(params, label=\"\"):\n",
        "    params = {**params, \"countTotal\": \"true\", \"format\": \"json\"}\n",
        "    resp = requests.get(BASE, params=params)\n",
        "    resp.raise_for_status()\n",
        "    data = resp.json()\n",
        "    print(f\"{label:<26} totalCount = {data['totalCount']:>6,}\")\n",
        "    return data"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "d1 = run({\"query.cond\": \"ADHD\"}, \"all trials\")"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "FSnzzVNCQSh3",
        "outputId": "79d17f8a-f5fa-4384-9cfa-7839cbbabaf9"
      },
      "execution_count": 31,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "all trials                 totalCount =  1,953\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "d2 = run({\"query.cond\": \"ADHD\",\n",
        "          \"filter.overallStatus\": \"COMPLETED\"}, \"+ completed\")"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "lJw3-3pVQS-M",
        "outputId": "1a69b61f-3208-40d7-f27f-b65c13010200"
      },
      "execution_count": 32,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "+ completed                totalCount =  1,246\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "d3 = run({\"query.cond\": \"ADHD\",\n",
        "          \"aggFilters\": \"phase:3\"}, \"+ phase 3\")"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "Qd0vWvX7QUew",
        "outputId": "7ea6b1a6-8c1b-4033-cc48-fc0f01085031"
      },
      "execution_count": 33,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "+ phase 3                  totalCount =    233\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [],
      "metadata": {
        "id": "vp5KKcwPQWIF"
      },
      "execution_count": null,
      "outputs": []
    }
  ]
}
