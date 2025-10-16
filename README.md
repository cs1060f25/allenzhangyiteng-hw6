# Company Formation Server

This server accepts company formation data and generates Articles of Incorporation for Delaware, California, and New York corporations and LLCs.

## Live Deployment

🚀 **Production URL**: https://company-formation-server-jet.vercel.app/

## Setup

1. Install the required dependencies:
```bash
pip install -r requirements.txt
```

2. Run the server:
```bash
python app.py
```

## API Usage

Send a POST request to `/form-company` with a JSON payload in the following format:

```json
{
    "company_name": "Acme Corp, Inc.",
    "state_of_formation": "DE",
    "company_type": "corporation",
    "incorporator_name": "John Smith"
}
```

### Validation Rules:
- Company name: Can contain alphanumeric characters, spaces, commas, periods, apostrophes, and ampersands
- State of formation: Must be a valid US state or territory code
- Company type: Must be either "corporation" or "LLC"
- Incorporator name: Required field

### Response:
- For Delaware, California, and New York corporations and LLCs: Returns a PDF file containing the appropriate formation document
- For other states/company types: Returns a 400 error indicating unsupported formation type

### Supported States and Types:
- **Delaware (DE)**: Corporations and LLCs
- **California (CA)**: Corporations and LLCs
- **New York (NY)**: Corporations and LLCs

## Example cURL Requests:

### Testing the Production Deployment:
```bash
# New York Corporation
curl -X POST https://company-formation-server-jet.vercel.app/form-company \
  -H "Content-Type: application/json" \
  -d '{"company_name": "Acme Corp, Inc.", "state_of_formation": "NY", "company_type": "corporation", "incorporator_name": "John Smith"}' > ny_corp.pdf

# New York LLC
curl -X POST https://company-formation-server-jet.vercel.app/form-company \
  -H "Content-Type: application/json" \
  -d '{"company_name": "Empire State, LLC", "state_of_formation": "NY", "company_type": "LLC", "incorporator_name": "Jane Doe"}' > ny_llc.pdf
```

### Testing Locally:
```bash
curl -X POST http://localhost:5000/form-company \
  -H "Content-Type: application/json" \
  -d '{
    "company_name": "Acme Corp, Inc.",
    "state_of_formation": "DE",
    "company_type": "corporation",
    "incorporator_name": "John Smith"
  }'
```
