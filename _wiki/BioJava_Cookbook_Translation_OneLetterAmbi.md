---
title: BioJava:Cookbook:Translation:OneLetterAmbi
permalink: wiki/BioJava%3ACookbook%3ATranslation%3AOneLetterAmbi
---

How can I retrieve the 1-Letter code of a translated sequence containing ambiguities?
-------------------------------------------------------------------------------------

In HIV context, population sequencing is done to detect mutations, which
could induce resistance against certain drug. So sequences from HIV
often contain ambiguities. The annotation for HIV mutation follows the
following convention: I47VA ("47" is the position in the reference
sequence, "I" the amino acid in the reference sequence and "V,A" the
amino acids in the sequence we look at).

This sample code shows how to retrieve the 1-Letter code needed for this
annotation at every position of the translated sequence:

```java import java.util.Iterator; import org.biojava.bio.BioException;
import org.biojava.bio.seq.DNATools; import
org.biojava.bio.seq.io.SymbolTokenization; import
org.biojava.bio.symbol.Alphabet; import
org.biojava.bio.symbol.FiniteAlphabet; import
org.biojava.bio.symbol.Symbol; import org.biojava.bio.symbol.SymbolList;

public class Main {

`   public static void main(String[] args) {`  
`       try {`  
`           // TODO code application logic here`  
`           SymbolList symL = DNATools.createDNA("atnatggnnatg");`  
`           SymbolList symL2 = DNATools.toProtein(symL);`

`           System.out.println("Translated sequence: " + symL2.seqString() + "\n");`

`           System.out.println("Show codons in three letter code taking ambiguities into account:");`  
`           for (Iterator i = symL2.iterator(); i.hasNext();) {`  
`               Symbol sym = (Symbol) i.next();`  
`               System.out.println("" + sym.getName());`  
`           }`

`           System.out.println("Show codons in one letter code: " + symL2.seqString());`

`           SymbolTokenization toke = symL2.getAlphabet().getTokenization("token");`  
`           for (Iterator i = symL2.iterator(); i.hasNext();) {`  
`               Symbol sym = (Symbol) i.next();`

`               Alphabet arg = sym.getMatches();`

`               for (Iterator i2 = ((FiniteAlphabet) arg).iterator(); i2.hasNext();) {`

`                   Symbol sym2 = (Symbol) i2.next();`

`                   //This will print out the one letter code:`  
`                   System.out.println("one letter code: " + toke.tokenizeSymbol(sym2));`

`               //This would print out the three letter code:`  
`               //System.out.println("name: " + sym2.getName());`  
`               }`  
`               System.out.println("\n");`  
`           }`  
`       } catch (BioException ex) {`  
`           ex.printStackTrace();`  
`       }`  
`   }`

} ```
