# ALCE-ASQA BENCHMARK

## 1. Description

`ALCE-ASQA` is different from the original `ASQA` dataset. The description of the original paper<sup>[1]</sup> on this dataset is as follows.
> ASQA<sup>[2]</sup> is a long-form factoid dataset. Each question is an ambiguous question from AmbigQA<sup>[3]</sup> and requires multiple short answers to cover different interpretations of the question. For example, the question “When did the US break away from England?” should be answered with both July 2, 1776 (declaration of independence) and September 3, 1783 (Treaty of Paris). The ambiguity nature of the questions necessitates synthesizing information from multiple documents. Stelmakh et al. crowdsourced long-form answers for each question to cover all short, disambiguated answers while providing essential background information. Human-written answers for ASQA have an average length of 65 words. Since most of the questions can be answered by Wikipedia, we use the 2018-12-20 Wikipedia snapshot as D. Using a small corpus allows researchers to deploy and study different retrieval methods at low cost, especially dense retrieval<sup>[4][5]</sup>.
> 
> We randomly select 1,000 examples from the development set of each dataset for ALCE. Our benchmark primarily assesses the citation capabilities of existing LLMs and does not provide training data, as there are no available examples that provide supervision for citations in these datasets.

## 2. Dataset

The ALCE-ASQA dataset consists of three versions: `GTR`, `DPR` and `Oracle`. Each versions contain 948 data entries with consistent questions. In the `GTR` and `DPR` version, each entry provides the top-100 passages retrieved using dense retrievers from the Wikipedia corpus. The `Oracle` version approximates golden passages through passages reranking, resulting in higher-quality passages compared to the previous version. Each passage is segmented into chunks of 100 words.

Additionally, each data entry includes annotated versions of `Summary` and `Snippet` generated by ChatGPT.

```
{
    "qa_pairs": [
        {
            "context": "No context provided",
            "question": "Who has the highest goals in men's world international football?",
            "short_answers": [
                "Daei",
                "Ali Daei"
            ],
            "wikipage": null
        },
        {
            "context": "No context provided",
            "question": "Who has the highest goals all-time in men's football?",
            "short_answers": [
                "Bican",
                "Josef Bican"
            ],
            "wikipage": null
        },
        {
            "context": "The first player to reach 100 international goals was Italian Elisabetta Vignotto. Abby Wambach scored 100 goals in 9 years, while Christine Sinclair reached the milestone in just under 10 years while Mia Hamm is the youngest player to score 100 international goals at the age of 26 years 185 days. Most played exclusively in the forward position, with Kristine Lilly and Michelle Akers having also played as midfielder. All players scored at a high average rate of more than one goal every three matches. International goals in this list should not include goals scored in penalty-shoot-out; see Penalty shootout (association football). Players who are currently active at international level are indicated in bold type background.",
            "question": "Who has the highest goals in women's world international football?",
            "short_answers": [
                "Sinclair",
                "Christine Sinclair"
            ],
            "wikipage": "List of women's footballers with 100 or more international goals ..."
        }
    ],
    "wikipages": [
        {
            "title": "International Federation of Football History & Statistics",
            "url": "https://en.wikipedia.org/wiki/International%20Federation%20of%20Football%20History%20%26%20Statistics"
        },
        {
            "title": "List of FIFA World Cup records and statistics",
            "url": "https://en.wikipedia.org/wiki/List%20of%20FIFA%20World%20Cup%20records%20and%20statistics"
        },
        {
            "title": "List of footballers with more than 50 international goals",
            "url": "https://en.wikipedia.org/wiki/List%20of%20footballers%20with%20more%20than%2050%20international%20goals"
        },
        {
            "title": "List of women's footballers with 100 or more international goals ...",
            "url": "https://en.wikipedia.org/wiki/List%20of%20women%27s%20footballers%20with%20100%20or%20more%20international%20goals"
        },
        {
            "title": "List of footballers with 500 or more goals",
            "url": "https://en.wikipedia.org/wiki/List%20of%20footballers%20with%20500%20or%20more%20goals"
        }
    ],
    "annotations": [
        {
            "knowledge": [],
            "long_answer": "Ali Dael has the highest goals in men's world international football with 109 goals. Josef Bican has the highest goals all-time in men's football and Christine Sinclair has the highest goals in women's world international football."
        },
        {
            "knowledge": [
                {
                    "content": "Sinclair is the world's all-time leader for international goals scored for men or women with 187 goals, and is one of the most-capped active international footballer with 300 caps.",
                    "wikipage": "Christine Sinclair"
                },
                {
                    "content": "Along with Cristiano Ronaldo, he is the world's joint all-time leading goalscorer in the history of men's international football with 109 goals scored for Iran.",
                    "wikipage": "Ali Daei"
                },
                {
                    "content": "Ronaldo holds the records for most goals (134) and assists (42) in the Champions League, most goals in the European Championship (14), and is currently tied with Ali Daei for most international goals (109).",
                    "wikipage": "Cristiano Ronaldo"
                },
                {
                    "content": "FIFA, the international governing body of football, have never released a list detailing the highest goalscorers and do not keep official records;[6][7] in 2020, they recognised Bican, an Austrian-Czech dual international who played between the 1930s and the 1950s,[8] as the record scorer with an estimated 805 goals,[9][10] while CNN, the BBC, France 24, and O Jogo all acknowledge that Bican's tally of 805 includes goals scored for reserve teams and in unofficial international matches.",
                    "wikipage": "List of footballers with 500 or more goals"
                }
            ],
            "long_answer": "The players with the highest all-time goals and highest men's and women's international football goals differ. The player with the highest all-time men's football goals is Josef Bican, who in 2020 was recognized by FIFA, the international governing body of football, as the record scorer with an estimated 805 goals. Christine Sinclair has the highest goals in women's international football with 187 and is the all-time leader for international goals scored for men or women. Cristiano Ronaldo and Ali Daei are currently tied for leading goalscorer in the history of men's international football with 109."
        }
    ],
    "sample_id": "-7013890438520559398",
    "question": "Who has the highest goals in world football?",
    "docs": [
        {
            "id": "6669150",
            "title": "Argentina\u2013Brazil football rivalry",
            "text": "\"Football Player of the Century\", by IFFHS International Federation of Football History and Statistics, 1999, \"South America Football Player of the Century\", by IFFHS International Federation of Football History and Statistics. Pel\u00e9's 1281 goals are recognized by FIFA as the highest total achieved by a professional footballer, although the Soccer Statistic Foundation (rssf) recognizes only 767 goals in official mode, occupying the third place after Josef Bican (805) and Romario (772). For his part, Maradona has been named the best soccer player in World Cup history both by The Times and FourFourTwo, publication that also rewarded him as the \"Best",
            "score": 0.73388671875,
            "summary": "Pel\u00e9 holds the record for the highest total goals achieved by a professional footballer with 1281 goals, recognized by FIFA. However, the Soccer Statistic Foundation recognizes only 767 goals in official mode, with Josef Bican and Romario having higher counts. Maradona has been named the best soccer player in World Cup history.",
            "extraction": "Pel\u00e9's 1281 goals are recognized by FIFA as the highest total achieved by a professional footballer."
        },
        {
            "id": "9416170",
            "title": "Godfrey Chitalu",
            "text": "have beaten Gerd M\u00fcller's record of 85 goals in a year, the Football Association of Zambia claimed that the world record actually pertained to Godfrey Chitalu who had scored 116 goals (possibly 117) during the 1972 calendar year and 107 during the 1972 season. The difference of goals is due to first 9 goals being scored before the season officially started. The Football Association of Zambia presented the evidence to FIFA but a spokesperson responded that they would ratify neither Lionel Messi's nor Chitalu's records as they do not keep statistical track of domestic competitions. Nonetheless, it could constitute the",
            "score": 0.7080078125,
            "summary": "Godfrey Chitalu had scored 116 goals (possibly 117) during the 1972 calendar year and 107 during the 1972 season, surpassing Gerd M\u00fcller's record of 85 goals. However, FIFA did not officially ratify either Chitalu's or Lionel Messi's records as they do not keep statistical track of domestic competitions.",
            "extraction": "Godfrey Chitalu has the highest goals in world football with 116 goals (possibly 117) during the 1972 calendar year and 107 during the 1972 season, according to the Football Association of Zambia."
        },
        ...
    ],
    "answer": "The players with the highest all-time goals and highest men's and women's international football goals differ. The player with the highest all-time men's football goals is Josef Bican, who in 2020 was recognized by FIFA, the international governing body of football, as the record scorer with an estimated 805 goals. Christine Sinclair has the highest goals in women's international football with 187 and is the all-time leader for international goals scored for men or women. Cristiano Ronaldo and Ali Daei are currently tied for leading goalscorer in the history of men's international football with 109.",
}
```

## 3. Metrics

In the original paper, the authors evaluated four metrics on the ASQA dataset: MAUVE, EM recall, Citation Recall, and Citation Precision. 

1. MAUVE<sup>[6]</sup>: MAUVE measures the similarity between two text distributions. Specifically, we concatenate the question and the model output and compare it to the distribution of question-gold-answer concatenation. **We will add this metric in future work.**
2. [EM recall](../../rageval/metrics/_answer_exact_match.py): EM recall calculates the recall of correct short answers by checking whether the short answers (provided by the dataset) are exact substrings of the generation.
3. [Citation Recall](../../rageval/metrics/_answer_citation_recall.py): Citation Recall determines if the result from LLM is entirely supported by cited passages.
4. [Citation Precision](../../rageval/metrics/_answer_citation_precision.py): Citation Precision detects citations that are irrelevant to the claim, but it does not require citing a minimal set and it permits citing redundant passages entailing similar claims.

Additionally, metrics such as ROUGE were also included in the evaluation, but no performance comparisons were made.

## 4. Usage

### 4.1 Prepare

Download and unzip the dataset, and install the RagEval tool.
```bash
script_dir=$(cd $(dirname $0);pwd)
cache_dir=$(dirname $(dirname $(dirname $script_dir)))/.rageval
wget -cP $cache_dir/datasets https://huggingface.co/datasets/princeton-nlp/ALCE-data/resolve/main/ALCE-data.tar
tar -xvf $cache_dir/datasets/ALCE-data.tar -C $cache_dir/datasets
python3 setup.py install
```

### 4.2 Generate examples

Replace api_key to your OpenAI api key in `run.sh` then run it to generate `gpt-3.5-turbo` response. The command is as follows:
```bash
python3 $script_dir/generate.py\
  --cache_path $cache_dir\
  --model gpt-3.5-turbo\
  --api_key "YOUR_API_KEY"\
  --dataset gtr\
  --method vanilla\
  --ndoc 5\
  --shot 2
```

You can also use local models for generation.
```bash
python3 $script_dir/generate.py\
  --cache_path $cache_dir\
  --model Llama-2-7b-chat-hf\
  --dataset gtr\
  --method vanilla\
  --ndoc 5\
  --shot 2
```

Arguements:
- `--cache_path`: The script automatically calculates the `cache_path`, so users generally don't need to specify it. The default path is the `.rageval` directory.
- `--model`: The model's name, currently supports OpenAI's API as well as open-source models like LLAMA.
- `--api_key`: When using OpenAI's API, the `api_key` parameter is required, otherwise, please ignore this parameter.
- `--max_length`: The maximum token count supported by the model.
- `--temperature/top_p`: The inference hyperparameters for LLM.
- `--dataset`: Version of the dataset: `gtr`, `dpr` or `oracle`.
- `--method`: Supports three generation methods: `vanilla`, `summary`, and `snippet`. The difference lies in the processing of the input documents.
- `--ndoc`: The number of documents provided to LLM during the generation process.
- `--shot`: The number of examples provided to LLM during the generation process.

### 4.3 Evaluation

You can download pre-generated result file from HuggingFace for evaluation.

```bash
python3 $script_dir/asqa_benchmark.py\
  --cache_path $cache_dir\
  --remote_split Llama_2_7b_chat_hf_vanilla_shot2_ndoc5
```

You can also specify locally saved result file for evaluation.

```bash
python3 $script_dir/asqa_benchmark.py\
  --cache_path $cache_dir\
  --local_file "YOUR_LOCAL_FILE"
```

Arguements:
- `--cache_path`: The script automatically calculates the `cache_path`, so users generally don't need to specify it. The default path is the `.rageval` directory.
- `--remote_split`: Download pplit dataset from [our huggingface dataset](https://huggingface.co/datasets/golaxy/rag-bench) to evaluate.
- `--local_file`: Specify locally saved result file to evaluate.

## 5. Performance

### 5.1 GTR
| Model           | Method          | MAUVE | EM Recall | Citation Recall | Citation Precision |
|-----------------|-----------------|-------|-----------|-----------------|--------------------|
| Llama-2-7b-chat | vanilla(5-psg)  | --    | 33.3474   | 55.9004         | 80.0420            |
| Llama-2-7b-chat | summary(5-psg)  | --    | --        | --              | --                 |
| Llama-2-7b-chat | summary(10-psg) | --    | --        | --              | --                 |
| Llama-2-7b-chat | snippet(5-psg)  | --    | --        | --              | --                 |
| Llama-2-7b-chat | snippet(10-psg) | --    | --        | --              | --                 |

### 5.2 DPR
| Model           | Method          | MAUVE | EM Recall | Citation Recall | Citation Precision |
|-----------------|-----------------|-------|-----------|-----------------|--------------------|
| Llama-2-7b-chat | vanilla(5-psg)  | --    | --        | --              | --                 |

### 5.2 Oracle
| Model           | Method          | MAUVE | EM Recall | Citation Recall | Citation Precision |
|-----------------|-----------------|-------|-----------|-----------------|--------------------|
| Llama-2-7b-chat | vanilla(5-psg)  | --    | --        | --              | --                 |


## 6 References
[1] Gao Tianyu, Yen Howard, Yu Jiatong and Chen Danqi. 2023. Enabling Large Language Models to Generate Text with Citations. Empirical Methods in Natural Language Processing (EMNLP).

[2] Ivan Stelmakh, Yi Luan, Bhuwan Dhingra, and Ming-Wei Chang. 2022. Asqa: Factoid questions meet long-form answers. arXiv preprint arXiv:2204.06092.

[3] Sewon Min, Julian Michael, Hannaneh Hajishirzi, and Luke Zettlemoyer. 2020. AmbigQA: Answering ambiguous open-domain questions. In Proceedings of the 2020 Conference on Empirical Methods in Natural Language Processing (EMNLP), pages 5783-5797, Online. Association for Computational Linguistics.

[4] Vladimir Karpukhin, Barlas Oguz, Sewon Min, Patrick Lewis, Ledell Wu, Sergey Edunov, Danqi Chen, and Wen-tau Yih. 2020. Dense passage retrieval for opendomain question answering. In Proceedings of the 2020 Conference on Empirical Methods in Natural Language Processing (EMNLP), pages 6769–6781, Online. Association for Computational Linguistics.

[5] Jianmo Ni, Chen Qu, Jing Lu, Zhuyun Dai, Gustavo Hernandez Abrego, Ji Ma, Vincent Zhao, Yi Luan, Keith Hall, Ming-Wei Chang, and Yinfei Yang. 2022. Large dual encoders are generalizable retrievers. In Empirical Methods in Natural Language Processing (EMNLP), pages 9844–9855.

[6] Krishna Pillutla, Swabha Swayamdipta, Rowan Zellers, John Thickstun, Sean Welleck, Yejin Choi, and Zaid Harchaoui. 2021. MAUVE: Measuring the gap between neural text and human text using divergence frontiers. In Advances in Neural Information Processing Systems.