# NAME

buildLoci

# SYNOPSIS

A utility to build gene loci (i.e., sets of overlapping transcripts) out of a transcript set.

**Usage example**:

`bedtools intersect -s -wao -a inGTF -b inGTF | buildLoci.pl - > test.loci.gff`

## INPUT

The input file is provided as first argument to the script. It consists in two ("left" and "right") GTF records per line, separated by a `tab`. This is typically the standard output produced by `bedtools intersect -wao -a inGTF -b inGTF` (`inGTF` being a single GTF file).

The flexibility of `bedtools` allows the user to build gene loci based on whatever definition they need, e.g., with or without respect to genomic strand (see `bedtools`'s `-s` option).

## OPTIONS

- **keepGeneid** = If set, any `gene_id` values present in the input will be kept in the output, under attribute `gene_id_bkp`.

## OUTPUT

One GTF line per unique "left" GTF record in the input, with a supplementary `gene_id` attribute (in the form of `LOC_XXXXXXXXXX`) appended to its 9th field.

Any gene\_id value present in the input will be overwritten, except if the `--keepGeneid` option is used.

# DESCRIPTION

Any pair of GTF records present within a line of input is assumed to represent overlapping features. Gene loci are then built based on these overlaps, i.e. the &lt;transcript\_id>s of both records are assigned the same arbitrary &lt;gene\_id> value in the output.

# DEPENDENCIES

Although not strictly necessary, [BEDTools](https://github.com/arq5x/bedtools2) is recommended, solely to provide input to `buildLoci.pl`.

# AUTHOR

Julien Lagarde, CRG, Barcelona, contact julienlag@gmail.com
