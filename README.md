# merge-a.pl
中間結果とBLAST検索（COG）・BLAST検索（RefSeq）・BLAST検索（TrEMBL）の結果から最
終結果を生成するスクリプト。実行にBioPerlが必要であるため、base imageとしてyookuda/bioperlを使用する。

## Usage
```usage
docker run \
    -v data_dir_path:/data \
    -v COG_DB_dir_path:/cog \
    -v RefSeq_DB_dir_path:/refseq \
    --rm \
    yookuda/merge_a \
        perl /scripts/merge-a.pl \
            --cog /data/<COG DBでのBLAST検索結果ファイル> \
            --trembl /data/<TrEMBL DBでのBLAST検索結果ファイル> \
            --ref /data/<RefSeq DBでのBLAST検索結果ファイル> \
            --whog /cog/whog \
            --myva /cog/myva \
            --gpff /refseq/microbial.*.protien.gpff.gz \
            --prefix /data/<output file prefix>
```
- BLAST検索結果ファイルは-outfmt "0" オプションで出力したものを使用する。
- 出力されるファイルは以下の通り。
    - &lt;output file prefix&gt;-a.gbk: GenBank flat file
    - &lt;output file prefix&gt;-a.embl: Embl flat file
    - &lt;output file prefix&gt;-a.annt
    - &lt;output file prefix&gt;-a.csv
    - &lt;output file prefix&gt;-a.ddbj: DDBJ flat file
