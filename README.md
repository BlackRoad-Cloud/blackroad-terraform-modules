# BlackRoad Terraform Modules

> Production-quality Terraform IaC module generation for AWS, GCP, and Azure.

## Features

- `TerraformModule` dataclass (name, provider, resource_type, variables, outputs)
- `generate_main_tf()`, `generate_variables_tf()`, `generate_outputs_tf()`
- `.tfvars` generation from Python dicts
- `plan_summary()` — parse JSON or text `terraform plan` output
- `cost_estimate()` — monthly/annual cost with provider pricing tables
- SQLite persistence for generated modules
- CLI: `new`, `cost`, `plan`, `list`

## Usage

```bash
# Generate a new AWS EC2 module
python src/terraform_modules.py new \
  --name ec2_cluster \
  --provider aws \
  --resource-type aws_instance \
  --output-dir ./modules

# Estimate cost
python src/terraform_modules.py cost \
  --provider aws \
  --resources '[{"type":"instance","count":3},{"type":"rds","count":1}]'

# Summarize terraform plan
python src/terraform_modules.py plan plan.json
```

## Module Output Structure

```
modules/ec2_cluster/
├── main.tf          # Provider + resource blocks
├── variables.tf     # Variable declarations
├── outputs.tf       # Output declarations
└── README.md        # Auto-generated docs
```

## Tests

```bash
pytest tests/ -v --cov=src
```
