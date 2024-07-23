# MultiCardioNER Evaluation Library

This repository contains the official evaluation library for the [MultiCardioNER Shared Task](https://temu.bsc.es/multicardioner).
MultiCardioNER is a shared task/challenge and set of resources focused on the multilingual adaptation of clinical NER systems to the cardiology domain.
For more information about the task, data, evaluation metrics, ... please visit the task's website.

This repository is heavily based on the [MedProcNER evaluation library](https://github.com/TeMU-BSC/medprocner_evaluation_library) by the same author.

## Requirements

To use this scorer, you'll need to have Python 3 installed in your computer. Clone this repository, create a new virtual environment and then install the required packages:

```bash
git clone https://github.com/nlp4bia-bsc/multicardioner_evaluation_library
cd multicardioner_evaluation_library
python3 -m venv venv/
source venv/bin/activate
pip install -r requirements.txt
```

The MultiCardioNER task data is available on [Zenodo](https://zenodo.org/doi/10.5281/zenodo.10948354). This includes the filename mapping file required to use this library and the Gold Standard test set data.

## Usage Instructions

This program compares two .TSV files, with one being the reference file (i.e. Gold Standard data provided by the task organizers) and the other being the predictions or results file (i.e. the output of your system). Your .TSV file needs to have the following structure:

- For all sub-tasks: filename, label, start_span, end_span, text

Since the task's original test set data masked the files' names, you will also need the mappings file, which is available on [Zenodo](https://zenodo.org/doi/10.5281/zenodo.10948354). This requirement might be changed in the future, but we decide to keep it for now to be faithful to the evaluation setting.

Once you have your predictions file in the appropriate format, the reference data ready and the mappings file, you can run the library from your terminal using the following command:

```commandline
python3 multicardioner_evaluation.py -r toy_data/ref/multicardioner_test_task1_toy.tsv -m multicardioner_test+background_fname-mapping.tsv -p toy_data/pred/multicardioner_test_task1_all_correct.tsv -t track1 -o toy_data/pred/
```

The output will be a .txt file saved in your desired location (`-o` option) with the following filename: multicardioner_results_{task}_{timestamp}.txt

These are the possible arguments:

+ ```-r/--reference```: path to Gold Standard TSV file with the annotations
+ ```-m/--mapping```: path to the TSV file with the mapping between the masked and the actual test set filenames (available on Zenodo).
+ ```-p/--prediction```: path to predictions TSV file with the annotations
+ ```-o/--output```: path to save the scoring results file
+ ```-t/--task```: subtask name (```task1```, ```task2_es```, ```task2_en``` or ```task2_it```). The evaluation for all of them is the done in the same way, this option only changes the output file's headers.
+ ```-v/--verbose```: whether to include the evaluation of every individual document in the scoring results file


## Citation
If you use the MultiCardioNER evaluation library or data, please cite:

@inproceedings{multicardioner2024overview,
title={{Overview of MultiCardioNER task at BioASQ 2024 on Medical Speciality and Language Adaptation of Clinical NER Systems for Spanish, English and Italian}},
author={Salvador Lima-López and Eulàlia Farré-Maduell and Jan Rodríguez-Miret and Miguel Rodríguez-Ortega and Livia Lilli and Jacopo Lenkowicz and Giovanna Ceroni and Jonathan Kossoff and Anoop Shah and Anastasios Nentidis and Anastasia Krithara and Georgios Katsimpras and Georgios Paliouras and Martin Krallinger},
booktitle={CLEF Working Notes},
year={2024},
editor = {Faggioli, Guglielmo and Ferro,  Nicola and  Galuščáková, Petra and  García Seco de Herrera, Alba}}

## Contact
If you have any questions or suggestions, please contact us at:

- Salvador Lima-López (<salvador [dot] limalopez [at] gmail [dot] com>)
