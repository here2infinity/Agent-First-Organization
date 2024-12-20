**1. Create Taskgraph and Initialize Worker**
```
python create.py --config ./app/app_config.json --output-dir ./app/app_service
```

```
python create.py --config ./tanzania_news_summary/tanzania_news_summary_config.json --output-dir ./tanzania_news_summary/tanzania_news_summary_service
```

**2. Start Chatting**
```
python run.py --input-dir ./app/app_service
```

```
python run.py --input-dir ./tanzania_news_summary/tanzania_news_summary_service
```

**3. Evaluation**

  * First, create api for the previous chatbot you built. It will start a api on the default port 8000.
    ```
    python model_api.py  --input-dir ./app/app_service
    ```
    ```
    python model_api.py --input-dir ./tanzania_news_summary/tanzania_news_summary_service
    ```

   * Fields:
      * `--input-dir`: The directory that contains the generated files
      * `--model`: The openai model type used to generate bot response. Default is `gpt-4o`. You could change it to other models like `gpt-4o-mini`.
      * `--port`: The port number to start the api. Default is 8000.

  * Then, start the evaluation process: 
    ```
    python eval.py \
    --model_api http://127.0.0.1:8000/eval/chat \
    --config ./app/app_config.json \
    --documents_dir ./app/app_service \
    --output-dir ./app/app_service
    ```
```
python eval.py \
--model_api http://127.0.0.1:8000/eval/chat \
--config ./tanzania_news_summary/tanzania_news_summary_config.json  \
--documents_dir ./tanzania_news_summary/tanzania_news_summary_service \
--output-dir ./tanzania_news_summary/tanzania_news_summary_service
```

    * Fields:
      * `--model_api`: The api url that you created in the previous step
      * `--config`: The path to the config file
      * `--documents_dir`: The directory that contains the generated files
      * `--output-dir`: The directory to save the evaluation results
      * `--num_convos`: Number of synthetic conversations to simulate. Default is 5.
      * `--num_goals`: Number of goals/tasks to simulate. Default is 5.
      * `--max_turns`: Maximum number of turns per conversation. Default is 5.
      * `--model`: The openai model type used to synthesize user's utterance. Default is `gpt-4o`. You could change it to other models like `gpt-4o-mini`.

run the following to get the chrome driver in 
https://stackoverflow.com/questions/63290844/how-to-run-selenium-chromedriver-from-python3-on-wsl2

wget -N https://storage.googleapis.com/chrome-for-testing-public/131.0.6778.108/linux64/chrome-linux64.zip

zip file obtained from: https://googlechromelabs.github.io/chrome-for-testing/