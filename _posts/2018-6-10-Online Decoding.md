---
layout : post
title : Online Decoding....
excerpt : Detailed procedure for Online2-wav-gmm-latgen-faster  
feature_image : "https://picsum.photos/2560/600?image=1042"
---

In this post we learn about how online decoding works.with this we would
create the online2-wav-gmm-latgen-faster in C++ for Spanish Model.

Let's create concept map of how decoding works...

 * Input audio features.

 * The MFCC features are computed on overlapping audio window. The new
   audio is used for shifting the audio window.

 *  Decode fixed number of frames.

 *  Get raw lattice and returns state-level lattice.

 *  Extracting  a word posterior lattice and returning log-likelihood
    of processed data. Also we can say , extract word level lattice from
    state level lattice.     

 *  When decoder is asked to perform decoding it needs to estimate log-likelihood
    for the states which should be explored  and it makes request to decodable
    interface.The decoder itself performs the search in state level space having
    the probabilities from the Decodable interface.

  * Online decoder returns word lattice with alignments in form of Compact Lattice.

  * The CompactLattice determinised at state level still may contain multiple
    paths for each word sequence encoded in the lattice. The Compact
    Lattice distinguishes each path not only according to the word labels on the path,
    but also according to the alignments    

  * The word posterior probability is converted from the likelihood of the words in
    word lattice. The word lattice obviously contains alternatives which were explored
    by the beam search during decoding the utterance.Similarly, the posterior
    probability is an approximation because the very low probable alternatives
    discarded by beam search are not considered. On the other hand, the discarded
    alternatives are so improbable so they almost do not influence the posterior
    probability.Presumably, the word posterior values are more impacted by
    inaccurate likelihood values taken from the Acoustic Model.

  * After this we just have to get the best hypothesis of words which were said.
    Technically, getting best word sequence.

  * Decoding parameter should be set before decoding ,I have used the same
     parameter mentioned in kaldi files.
      Example parameter such as ;

               beam,

               lattice-beam = (this affects speed of lattice extraction)

               , max-active-state =  (act as threshold for worst case scenario)       

###### Problems Faced

 * While compiling this file I face the error saying no matching function for
   call.You can view it in gist . Pointer is towards adaptation_state so ,
   I thought probably there must not be any parameter like "adaptation_state"
   But what I saw in online2-wav-gmm-latgen-faster.cc on kaldi website ,they
   have declared the same variable "adaptation_state" in SingleUtteranceGmmDecoder.
   No idea what should be done here.(Line 127 - 130)

{% gist wkranti/182babc6e06920bde830103069e5e7b0 %}

{% gist wkranti/d7d43d3389bc8cf89936c14793fafa2f %}   
