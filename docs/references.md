# References

## Software designs used as examples

- Kim, S.-J., Suh, N. P., Kim, S.-G. (1991). *Design of software systems based
  on axiomatic design.* Robotics & Computer-Integrated Manufacturing 8(4),
  243–255. doi:10.1016/0736-5845(91)90036-R.
  - The library system (pp. 246–249), in `examples/library_system/`.
  - The rib design software (pp. 249–251), in `examples/rib_design.ad.hcl`.
  - Known issues in the paper:
    - p. 247 prints "FR11 and FR22" where it means FR11 and FR12.
    - pp. 247–248 call the search OR, but describe the common domain of the
      keywords (AND).
    - p. 248 keeps the coupled search design only to show feedback, and says
      that a real design would look for an uncoupled one.
    - The synonym dictionary works only under the assumption that it is
      "sufficiently powerful".
    - Fig. 9 has an arrow from the expert system to M12 that the paper does
      not explain.
  - The paper treats DPs mostly as key input data and subroutines as PVs.
- Hintersteiner, J. D., Nain, A. S. (1999). *Integrating software into
  systems: an axiomatic design approach.*
  https://axiomaticdesign.com/technology/papers/eda99.pdf
  - Robot calibration software, top level only, in
    `examples/robot_calibration.ad.hcl`. It defines four software roles:
    program, interface, control logic and support.
  - The matrix in our example comes from a garbled text extraction, so check
    it against the original figure.

## Method

- Oh, H. L. (2016). Mathematical exposition of the design axioms.
  doi:10.1007/978-3-319-32388-6_2. The Jacobian criterion |J| ≠ 0.
  One DP per FR is sufficient but not necessary.
- Fradinho, J., Gonçalves-Coelho, A. (2021). The Information Axiom and robust
  design. doi:10.1007/978-3-030-49232-8_11.
- Farid, A. M. (2016). An engineering systems introduction to Axiomatic
  Design. doi:10.1007/978-3-319-32388-6_1. Maps AD terms to SysML.
- Thompson, M. K. (2014). Where is the "why" in Axiomatic Design? Why the
  language has `why` and `because`.
- Lindholm, D., Tate, D., Harutunian, V. (1999). Consequences of design
  decisions in Axiomatic Design. DP choices create new constraints and FRs.
- Park, C. Y., Matsumoto, S., Park, H. S. (2026). When to stop decomposing:
  LLM-assisted quality gates. doi:10.1109/access.2026.3683195.
- Gonçalves-Coelho, A. et al. (2012). Tackling redundant design solutions
  through axiomatic design. doi:10.1007/S12541-012-0241-X. On designs with
  more DPs than FRs.

## Tools and representation

- Harutunian, V. (1996). Representation methods for an axiomatic design
  process software. MIT thesis, https://dspace.mit.edu/handle/1721.1/39768.
  It names relational, inferential, inheritable and procedural knowledge.
- Kim, T. (1995). Implementation of axiomatic design theory. MIT thesis,
  http://dspace.mit.edu/handle/1721.1/34098. A design environment for AD that
  was itself designed with AD.
- Guenov, M. D., Barker, S. G. (2004). Requirements-driven design
  decomposition. doi:10.1115/DETC2004-57287. The design matrix and the DSM
  co-evolve.
- Wang, C.-Y., Liu, A., Lu, S. (2019). Building a numerical design matrix.
  doi:10.1051/MATECCONF/201930100011. Graded 0-1-3-9 levels.
- Zhang, X. et al. (2025). An axiomatic system engineering design method
  based on NSGA-II. doi:10.1038/s41598-025-17689-5. AD in SysML.
- Koh, E. C. Y. (2023). Using an LLM to generate a DSM.
  doi:10.48550/arxiv.2312.04134. 77% of the entries reproduced, so treat
  LLM-proposed influences as unconfirmed.

## DSL design and architecture drift

- Karsai, G. et al. (2009). Design guidelines for domain-specific languages.
  arXiv:1409.2378. Avoid conceptual redundancy.
- Frank, U. (2013). Domain-specific modeling languages: requirements analysis
  and design guidelines. doi:10.1007/978-3-642-36654-3_6.
- Buchgeher, G., Weinreich, R. (2009). Connecting architecture and
  implementation. doi:10.1007/978-3-642-05290-3_44.
- Wohlrab, R. et al. (2019). Improving the consistency and usefulness of
  architecture descriptions. doi:10.1109/ICSA.2019.00024.
