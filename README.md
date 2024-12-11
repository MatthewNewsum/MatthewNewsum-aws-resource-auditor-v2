# AWS Resource Auditor

A Python tool for auditing AWS resources across multiple regions and services.

## Installation

1. Clone the repository
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Prerequisites

- Python 3.6+
- Valid AWS credentials configured (via environment variables, AWS CLI configuration, or IAM role)
- Required Python packages:
  - boto3
  - pandas
  - xlsxwriter

## Usage

Run the script with optional parameters:

```bash
python main.py [--regions REGIONS] [--services SERVICES] [--output-dir OUTPUT_DIR]
```

### Parameters

- `--regions`: Comma-separated list of AWS regions or "all" (default: "all")
- `--services`: Comma-separated list of services to audit or "all" (default: "all")
- `--output-dir`: Directory for output files (default: "results")

### Available Services

- bedrock
- dynamodb
- ec2
- iam
- lambda
- rds
- s3
- vpc

## Examples

Audit all services in all regions:
```bash
python main.py
```

Audit specific services in specific regions:
```bash
python main.py --regions us-east-1,us-west-2 --services ec2,rds,vpc
```

Custom output directory:
```bash
python main.py --output-dir my-audit-results
```

## Output

The tool generates two report files:

### 1. JSON Report (`aws_inventory_TIMESTAMP.json`)
- Raw audit data in JSON format
- Complete resource details

### 2. Excel Report (`aws_inventory_TIMESTAMP.xlsx`)
- Formatted spreadsheet with multiple worksheets
- Resource summaries and detailed views
- Regional resource usage matrix

## Excel Report Worksheets

- IAM Users/Roles/Groups
- S3 Buckets
- EC2 Instances
- RDS Instances
- VPC Resources
- Lambda Functions
- DynamoDB Tables
- Bedrock Models
- Resource Usage by Region
- Resource Counts
- Region Summary
- Region Details

## Error Handling

The tool handles various error scenarios:
- Invalid regions
- Service availability issues
- Authentication/permission problems
- Resource access errors

Errors are logged and included in the final reports.

## Threading

The tool uses concurrent execution for improved performance:
- Default maximum worker threads: 10
- Configurable via source code (DEFAULT_MAX_WORKERS)