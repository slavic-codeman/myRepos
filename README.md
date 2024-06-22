# Lab4 Description
本次Lab主要有六个py文件:dataprocess.py,Sparse.py,examples.py,csv_process.py,main.py,baseline.py
## 依赖项安装
建议Python>=3.8避免可能存在的不兼容性。主要使用的外部库通过以下命令安装
```
pip install openai rank-bm25 tqdm

```
如果使用conda虚拟环境，也可以使用
```
conda create -n myenv python=3.10
conda activate myenv
conda install openai rank-bm25 tqdm
```
进行安装，并且推荐这种方式，因为这可以避免污染不同的Python环境
## dataprocess.py
主要是json文件读取和写入函数，以及对dictionary_za2zh.jsonl的数据转换，便于输入到LLM中，例如由
```
    {"za_word": "a", "zh_meanings": ["乌鸦", "呀", "呢"], "source": "https://zha_zho.en-academic.com/001", "zh_meanings_full": ["乌鸦 [与roegga同]", "呀 Caezgya vaiq daeuj ～！大家快来呀!", "(【见】 le) 呢 [语气词, 表示疑问]"]}
```
变为
```
    {
        "za": "a",
        "zh": "乌鸦;呀;呢"
    },
```
这将得到整理好的dic_org.json文件。
### 依赖项
仅需要Python自带的json库。

## Sparse.py
完成对单个query在平行语料库找相似例句，包括bm25和random两种策略。
### 依赖项
主要依赖rank-bm25库。

## examples.py
调用dataprocess.py中的load_json函数和Sparse.py中的选择函数，在get_prompt函数中得到每个query对应的单词示例和句子示例，调用create_prompt函数得到可以直接用于LLM的API的数据格式。
### 依赖项
依赖dataprocess.py和Sparse.py两个文件。

## csv_process.py
基于经验规则的csv文件后处理，去除输出中的多余部分。
### 依赖项
Python自带的csv库

## main.py
调用LLM完成对test_data.json的翻译，保存结果和prompts内容，可以改变sample变量从而改变选择例句的方法。
### 依赖项
openai和tqdm库，以及examples.py,dataprocess.py,csv_process.py文件。
### 代码运行
在文件夹目录终端中输入
```
python main.py
```
即可完成对test_data.json的翻译。

## baseline.py
在不提供示例的情况下，让LLM完成对test_data.json的翻译。
### 依赖项
openai和tqdm库，以及dataprocess.py,csv_process.py文件。
### 代码运行
在文件夹目录终端中输入
```
python baseline.py
```
即可完成对test_data.json的翻译，可以将生成的结果与main.py生成的结果进一步对比。
