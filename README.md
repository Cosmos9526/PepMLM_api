# PepMLM

## Description

PepMLM is a machine learning-based model for generating short peptide sequences that can act as binders to target proteins. Given a protein sequence and a set of parameters, PepMLM predicts peptide binders and returns them ranked by a pseudo-perplexity score, allowing you to identify promising peptides for further validation.

## Features

* Generates peptide sequences based on input protein sequences.
* Provides a FastAPI server to serve the model.
* Supports batch input processing.

## Project Structure

* `generation.py`: Implements peptide generation using a trained model.
* `app.py`: FastAPI-based server for generating peptides via API requests.
* `entrypoint.sh`: Script to launch the FastAPI server.
* `Dockerfile`: Configuration for containerizing the application.

## Running with Docker

You can pull and run the container directly:

```bash
docker pull cosmos9526/peptide-gan:latest
docker run -p 8000:8000 cosmos9526/peptide-gan:latest
```

## API Usage

### Endpoint: Generate Peptide

**URL:** `POST /generate/`

**Request Body:**

```json
{
        "protein_seq": "TQVCTGTDMKLRLPASPETHLDMLRHLYQGCQVVQGNLELTYLPTNASLSFLQDIQEVQGYVLIAHNQVRQVPLQRLRIVRGTQLFEDNYALAVLDNGDPLNNTTPVTGASPGGLRELQLRSLTEILKGGVLIQRNPQLCYQDTILWKDIFHKNNQLALTLIDTNRSRACHPCSPMCKGSRCWGESSEDCQSLTRTVCAGGCARCKGPLPTDCCHEQCAAGCTGPKHSDCLACLHFNHSGICELHCPALVTYNTDTFESMPNPEGRYTFGASCVTACPYNYLSTDVGSCTLVCPLHNQEVTAEDGTQRCEKCSKPCARVCYGLGMEHLREVRAVTSANIQEFAGCKKIFGSLAFLPESFDGDPASNTAPLQPEQLQVFETLEEITGYLYISAWPDSLPDLSVFQNLQVIRGRILHNGAYSLTLQGLGISWLGLRSLRELGSGLALIHHNTHLCFVHTVPWDQLFRNPHQALLHTANRPEDECVGEGLACHQLCARGHCWGPGPTQCVNCSQFLRGQECVEECRVLQGLPREYVNARHCLPCHPECQPQNGSVTCFGPEADQCVA",
,
    "peptide_length": 15,
    "top_k": 3,
    "num_binders": 4
}
```

**Response Example:**

```json
{
    "Binder": ["VSVGDLYLSHHACHG", "VSVIDELNSHHACHX"],
    "Pseudo Perplexity": [19.78339159265771, 16.451296854214522]
}
```
Interpretation: The second binder (VSVIDELNSHHACHX) has a lower pseudo-perplexity score (16.45) than the first binder (19.78), so the model is more confident that the second peptide is a better fit according to its learned patterns.

## References

* Project inspired by [PepMLM](https://github.com/programmablebio/pepmlm).
* See also this article on peptide-based design: [PMC10593082](https://pmc.ncbi.nlm.nih.gov/articles/PMC10593082/).

---

*Author: Milad Bagheri*

> Powered by passion, coffee, open source, and Iranian tea ☕️
