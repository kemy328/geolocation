# patients_geolocation
Project to locate patients in order to facilitate their home appointments by medical specialists

IT Solution development company has a team of 7 developers working on this project. The goal is to set up a software for geolocation of patients for their assistance by doctors. The application is for medical doctors and patients 

Developers use java language to write the code and push it into a private github repository. They use maven as build to tool to compile the source code in archaic way.

The manager of the IT solution development company needs to recruit you as a DevOps Engineer on this project.

The primary mission within the team is to set the source code analysis for this project.

# Instructions on how set up and use SOPS

## Setting up sops in order to encrypt and decrypt secret files:

   1.   Download sops using the following command:

        ```bash
        brew install sops
        ```
   2.   setting sops in development environment:

        SOPS encrypt and decrypt files using various key sources (GPG, AWS KMS, GCP KMS, …). For structured data, such as YAML, JSON, INI and ENV files, it will encrypt values, but not mapping keys. For YAML files, it also encrypts comments.
        
        ###  Setting sops with gpg:

           - if you don't already have a gpg key, follow this link to create one https://docs.gitlab.com/ee/user/project/repository/gpg_signed_commits/

           - create a .sops.yaml file

             ```
             ---
                creation_rules:
                    - path_regex: path/to/existing/            ###COMMENT: The path_regex checks the path of the encrypting file relative to the .sops.yaml config file. So basically matching the path starting from the `.sops.yaml` it belongs to. 

                      pgp: 'F4C60A55C2D8020CE371FF49AE3E43AE1A92015C' # (this is the key id)
                      encrypted_regex: '^(data|stringData)$'
            ```

          ###  setting up sops with kms

           - create a .sops.yaml file:

            ```bash
                ---
                creation_rules:
                    - path_regex: path/to/existing/            ###COMMENT: The path_regex checks the path of the encrypting file relative to the .sops.yaml config file. So basically matching the path starting from the `.sops.yaml` it belongs to.

                    kms: 'arn:aws-us-gov:kms:us-gov-west-1:235856440647:key/224a54fc-8440-414d-b73c-364522dd8d96'
                    encrypted_regex: '^(data|stringData)$'
            ```

## Encrypt and Decrypt a file 

We use the key described in a `.sops.yaml` file to encrypt and decrypt a file. When encrypting/decrypting a file, we always want to make sure we specify the `path_regex` within the `.sops.yaml` file. In case we want to leave the `path_regex` blank, it's recommended to put the `.sops.yaml` in the same directory with the file we want to encrypt/decrypt.

The following commands are used to encrypt and decrypt a file after a creating a sops.yaml file:

   Encrypting a file:

        ```bash
        sops -e -i <filename>
        ```

   Decrypting a file
        ```bash
        sops -i -d <filename>
        ```
