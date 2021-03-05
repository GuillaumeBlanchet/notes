# Installing the latest version of AWS CLI on Linux:

    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    unzip awscliv2.zip
    sudo ./aws/install

# Listing keys with aws cli:

    /usr/local/bin/aws s3api list-objects --output text --bucket icann-tcm --query 'Contents[].[Key]'

To list them inside a file, pipe the previous command in:

    /usr/local/bin/aws s3api list-objects --output text --bucket icann-tcm --query 'Contents[].[Key]' | pv -l > BUCKET.keys

# Deleting "efficiently" a folder:

    aws s3 sync --delete "local-empty-dir/" "s3://my_bucket/path-to-clear"

# Listing a folder:

    aws s3 ls s3://bucket/folder
