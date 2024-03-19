# Results

## GCG Individual attacks

>  optimizing over a single suffix and aggregating both gradients and losses to select top-k token substitutions and the best replacement at each step.

```
cd GCG/experiments
python -u main.py \
--config="configs/individual_{target_model}.py" \
--config.train_data="../../data/harmful_behaviors_custom.csv" \
--config.result_prefix="output/attacks/gcg/gcg_individual_{target_model}"
```

With `{target_model}` being `vicuna_13B`.

See [gcg_individual_vicuna_13B_20240319-10_16_58.json](./GCG/gcg_individual_vicuna_13B_20240319-10_16_58.json)

## PAIR

> The attacker generates candidate prompts to jailbreak the target, which then generates responses. These prompts and responses are evaluated for jailbreak scoring. If unsuccessful, the attacker iteratively refines prompts based on feedback from the target. <!-- The process involves attack generation, target response, jailbreak scoring, and iterative refinement steps, leading to a sustained conversation between the attacker and the target models. -->


```
python -m attacks.pair \
--harmful_behavior_path ./data/harmful_behaviors_custom.json \
--save_output_path {attack_output} \
--target_model {target_model} \
--defense_method {defense_method}
```

Where `{target_model}` is `vicuna`, `{defense_method}` is `backtranslation`.

See [PAIR_vicuna_backtranslation](./PAIR/PAIR_vicuna_backtranslation.json)

## AutoDAN

> Uses Genetic Algorithm (GA) to maximize the prompt's fitness score, which is defined as the likelihood of generating specific responses or outputs from the language model based on the jailbreak prompts provided. 

```
python attacks/autodan.py \
--harmful_behavior_path data/harmful_behaviors_custom.json \
--save_output_path {attack_output} \
--target_model {target_model}
```

Where `{target_model}` is `vicuna-13b-v1.5`.

See [DAN_attack_output.json](./AutoDAN/DAN_attack_output.json)
