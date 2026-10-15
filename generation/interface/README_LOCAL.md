# ReviewGPT (LitLLM) – local app with custom date-range search

## Run on your machine (localhost)
```bash
cd generation/interface
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...        # required (keyword extraction, re-ranking, generation)
export S2_API_KEY=...               # optional, avoids Semantic Scholar rate limits
python gradio_app.py                # -> http://127.0.0.1:7860
# options: --port 8080   --host 0.0.0.0 (expose on LAN)   --share (public gradio.live link)
```

## Run in Google Colab
```python
!git clone https://github.com/LitLLM/litllms-for-literature-review-tmlr
# upload the modified gradio_app.py + requirements.txt into generation/interface/ (or apply the patch)
%cd litllms-for-literature-review-tmlr/generation/interface
!pip install -q -r requirements.txt
import os; os.environ["OPENAI_API_KEY"] = "sk-..."   # or use Colab Secrets
!python gradio_app.py --share
```

## Date Range Filter
Use **From date** / **To date** in the left panel. Each takes `YYYY`, `YYYY-MM` or `YYYY-MM-DD`;
leave one blank for an open-ended range (e.g. From `2021`, To blank = 2021 onwards).

- Keyword / LLM-keyword search: sent to Semantic Scholar as `publicationDateOrYear`.
- Seed-paper recommendations: S2 has no date parameter there, so the app fetches 500
  recommendations and filters them locally. The seed paper itself is always listed first.
