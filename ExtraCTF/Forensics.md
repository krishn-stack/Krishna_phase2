# Riddle Registry:
Challenge given with a confidential.pdf file and asked to recover the flag.

## Flag:
```
picoCTF{puzzl3d_m3tadata_f0und!_c999e2a4}
```

## My Approach:
- Opened pdf file on an online pdf viewer.
- Got nothing behind the black lines in the pdf.
- Searched for .pdf file details.
- In Author details, there was some giberrish text so it needed to be decoded.

```
krishna@ULTRON:/mnt/c/Users/Krishna/Downloads$ strings confidential.pdf
%PDF-1.7
1 0 obj
/Type /Pages
/Count 1
/Kids [ 4 0 R ]
endobj
2 0 obj
/Producer (PyPDF2)
/Author (cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOTk5ZTJhNH0\075)
endobj
3 0 obj
/Type /Catalog
/Pages 1 0 R
endobj
4 0 obj
/Type /Page
/Resources <<
/Font <<
/F1 5 0 R
```
- Opened ```https://www.base64decode.org/``` and decoded the text.

## My Learnings:
- Looking for the metadata of the .pdf file.
- decoding the metadata.
