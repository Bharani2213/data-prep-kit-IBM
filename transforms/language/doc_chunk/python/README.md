# Chunk documents Transform 

This transform is chunking documents. It supports multiple _chunker modules_ (see the `chunking_type` parameter).

When using documents converted to JSON, the transform leverages the [Quackling](https://github.com/DS4SD/quackling) `HierarchicalChunker`
to chunk according to the document layout segmentation, i.e. respecting the original document components as paragraphs, tables, enumerations, etc.
It relies on documents converted with the Docling library in the [pdf2parquet transform](../pdf2parquet) using the option `contents_type: "application/json"`,
which provides the required JSON structure.

When using documents converted to Markdown, the transform leverages the [Llama Index](https://docs.llamaindex.ai/en/stable/module_guides/loading/node_parsers/modules/#markdownnodeparser) `MarkdownNodeParser`, which is relying on its internal Markdown splitting logic.


## Running

### Parameters

The transform can be tuned with the following parameters.


| Parameter  | Default  | Description  |
|------------|----------|--------------|
| `chunking_type`        | `dl_json` | Chunking type to apply. Valid options are `li_markdown` for using the LlamaIndex [Markdown chunking](https://docs.llamaindex.ai/en/stable/module_guides/loading/node_parsers/modules/#markdownnodeparser), `dl_json` for using the [Docling JSON chunking](https://github.ibm.com/DeepSearch/quackling). |
| `content_column_name_key`        | `contents` | Name of the column containing the text to be chunked. |
| `output_chunk_column_name_key`   | `contents` | Column name to store the chunks in the output table. |
| `output_jsonpath_column_name_key`| `doc_jsonpath` | Column name to store the document path of the chunk in the output table. |
| `output_pageno_column_name_key`  | `page_number` | Column name to store the page number of the chunk in the output table. |
| `output_bbox_column_name_key`    | `bbox` | Column name to store the bbox of the chunk in the output table. |

When invoking the CLI, the parameters must be set as `--doc_chunk_<name>`, e.g. `--doc_chunk_column_name_key=myoutput`.


### Running the samples
To run the samples, use the following `make` targets

* `run-cli-sample` - runs src/doc_chunk_transform.py using command line args
* `run-local-sample` - runs src/doc_chunk_local.py

These targets will activate the virtual environment and set up any configuration needed.
Use the `-n` option of `make` to see the detail of what is done to run the sample.

For example, 
```shell
make run-cli-sample
...
```
Then 
```shell
ls output
```
To see results of the transform.

### Transforming data using the transform image

To use the transform image to transform your data, please refer to the 
[running images quickstart](../../../../doc/quick-start/run-transform-image.md),
substituting the name of this transform image and runtime as appropriate.
