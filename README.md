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
    - Epochs: 35
Final Test Accuracy: 65.73%
Train accuracy: 87.26%
ჰგავს overfitting-ს, ამიტომ დავამატე dropout და შევამცირე lr=0.001-დან lr=0.0005-მდე.
შედეგად Train accuracy შემცირდა და გახდა 71.94%, Final Test Accuracy შენარჩუნდა 65.31%. ვარიაცია შემცირდა.
შემდეგ ვცადე შემდეგი ცვლილებები:
    - გავზარდე Spatial Dropout convolutional layer-ებისთვის
    - გავზარდე weight decay უფრო ძლიერი L2 რეგულარიზაციისთვის
    - დავამატე learning rate-ის scheduler
შედეგი: 
    Train Loss: 0.7810, Accuracy: 70.80%
    Val Loss: 1.0479, Accuracy: 63.74%
მოდელი თავიდან კარგად სტაბილურად სწავლობს თუმცა დაახლოებით 15-20 იტერაციის შემდეგ ვამჩნევ ოვერფიტინგს, რადგან ტრეინ აქურესი იზრდება და ველიდეიშენი მცირდება.
sgd ოპტიმიზაციაც ვცადე მაგრამ ვალიდეიშენ აქურესი 61.58%ზე ავიდა, ამიტომ საუკეთესო მოდელი მაინც თავდაპირველი გამოდგა.
