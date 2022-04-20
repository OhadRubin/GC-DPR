

## how to recreate
0. split wikipedia into `/parsed_dumps/*/wiki_*`
1. chunk wikipedia with `src/chunk_wiki.py`
2. to index wikipedia first change the format of the chunks into a format pyserini likes with `src/to_jsonl.py` (20 minutes).
3. perform the index calculation with the following (~22 minutes):
```
export JAVA_HOME=/a/home/cc/students/cs/ohadr/netapp/jdk-11.0.12
export JVM_PATH=/a/home/cc/students/cs/ohadr/netapp/jdk-11.0.12/lib/server/libjvm.so
python -m pyserini.index   --input /home/joberant/home/ohadr/4TB_SSD/chunks_new \
--collection JsonCollection   --generator DefaultLuceneDocumentGenerator   --index /home/joberant/home/ohadr/4TB_SSD/indexes/wikipedia_chunks_jsonl_new \
--threads 100   --storePositions --storeDocvectors --storeRaw --storeContents
```
4. couple the proofs with the chunks with `src/simple_index.py` (~5 hours).
5. change to dpr format with `src/to_dpr.py` (~5 minutes).
