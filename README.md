დავიწყე ტრეინ დატასეტის დასპლიტვით 60:20:20 თანაფარდობით. 
შევქმენი PyTorch Dataset class (`FERDataset`) შემდეგი ფუნქციონალით:
  - აკონვერტირებს პიქსელ სტრინგებს 48×48 numpy მასივებად
  - data augmentation (flips/rotations)
  - პიქსელ ველიუების ნორმალიზაცია (μ=0.5, σ=0.5)
class FERModel(nn.Module):
    Residual CNN with:
    - 3 convolutional blocks
    - Batch normalization
    - Global average pooling
    - 7-class output
Training Setup:
    - Loss: CrossEntropyLoss
    - Optimizer: AdamW (lr=0.001)
    - Scheduler: OneCycleLR
    - Batch size: 64
    - Epochs: 50
Final Test Accuracy: 66.39%
Train accuracy: 87.26%
ჰგავს overfitting-ს, ამიტომ ვცადოთ 
