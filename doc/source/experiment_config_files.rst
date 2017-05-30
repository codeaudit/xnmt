Experiment Configuration File Format
------------------------------------

Configuration files are in `YAML dictionary format <https://docs.ansible.com/ansible/YAMLSyntax.html>`_.

Top-level entries in the file correspond to individual experiments to run. Each
such entry must have four subsections: ``experiment``, ``train``, ``decode``,
and ``evaluate``. Options for each subsection are listed below.

There can be a special top-level entry named ``defaults``; if it is
present, parameters defined in it will act as defaults for other experiments
in the configuration file.

If any string option includes "<EXP>" this will be over-written by the name of the experiment.

Option Tables
=============

experiment
~~~~~~~~~~

+--------------------+-----------------------------------------------------------------+------+-----------+
| Name               | Description                                                     | Type | Default   |
+====================+=================================================================+======+===========+
| model_file         | Location to write the model file                                | str  | <EXP>.mod |
+--------------------+-----------------------------------------------------------------+------+-----------+
| hyp_file           | Location to write decoded output for evaluation                 | str  | <EXP>.hyp |
+--------------------+-----------------------------------------------------------------+------+-----------+
| out_file           | A file for writing stdout logging output                        | str  | <EXP>.out |
+--------------------+-----------------------------------------------------------------+------+-----------+
| err_file           | A file for writing stderr logging errput                        | str  | <EXP>.err |
+--------------------+-----------------------------------------------------------------+------+-----------+
| eval_metrics       | Comma-separated list of evaluation metrics (bleu/wer/cer)       | str  | bleu      |
+--------------------+-----------------------------------------------------------------+------+-----------+
| **run_for_epochs** | How many epochs to run each test for                            | int  |           |
+--------------------+-----------------------------------------------------------------+------+-----------+
| eval_every         | Evaluation period in iters, or 0 for never evaluating.          | int  | 0         |
+--------------------+-----------------------------------------------------------------+------+-----------+

decode
~~~~~~

+--------------------+-----------------------------------------------------------------+------+-----------+
| Name               | Description                                                     | Type | Default   |
+====================+=================================================================+======+===========+
| **source_file**    | path of input source file to be translated                      | str  |           |
+--------------------+-----------------------------------------------------------------+------+-----------+
| input_format       | format of input data: text/contvec                              | str  | text      |
+--------------------+-----------------------------------------------------------------+------+-----------+
| post_process       | post-processing of translation outputs: none/join-char/join-bpe | str  | none      |
+--------------------+-----------------------------------------------------------------+------+-----------+

evaluate
~~~~~~~~

+--------------------+-----------------------------------------------------------------+------+-----------+
| Name               | Description                                                     | Type | Default   |
+====================+=================================================================+======+===========+
| **ref_file**       | path of the reference file                                      | str  |           |
+--------------------+-----------------------------------------------------------------+------+-----------+

train
~~~~~

+-----------------------+-----------------------------------------------------------------+------+-----------+
| Name                  | Description                                                     | Type | Default   |
+=======================+=================================================================+======+===========+
| eval_every            |                                                                 | int  | 1000      |
+-----------------------+-----------------------------------------------------------------+------+-----------+
| batch_size            |                                                                 | int  | 32        |
| batch_strategy        |                                                                 | str  | src       |
| **train_source**      |                                                                 | str  |           |
| **train_target**      |                                                                 | str  |           |
| **dev_source**        |                                                                 | str  |           |
| **dev_target**        |                                                                 | str  |           |
| pretrained_model_file | Path of pre-trained model file                                  | str  |           |
| input_format          | Format of input data: text/contvec                              | str  | text      |
| default_layer_dim     | Default size to use for layers if not otherwise overridden      | int  | 512       |
| input_word_embed_dim  |                                                                 | int  |           |
| output_word_embed_dim |                                                                 | int  |           |
| output_state_dim      |                                                                 | int  |           |
| output_mlp_hidden_dim |                                                                 | int  |           |
| attender_hidden_dim   |                                                                 | int  |           |
| encoder_hidden_dim    |                                                                 | int  |           |
| trainer               |                                                                 | str  | sgd       |
| eval_metrics          |                                                                 | str  | bleu      |
| encoder_layers        |                                                                 | int  | 2         |
| decoder_layers        |                                                                 | int  | 2         |
| encoder_type          |                                                                 | str  | BiLSTM    |
| decoder_type          |                                                                 | str  | LSTM      |
| residual_to_output    | Whether to add a residual connection to the output layer        | bool | True      |
+-----------------------+-----------------------------------------------------------------+------+-----------+